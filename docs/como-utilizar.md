# Como Utilizar

## Organização de diretórios

Todo o armazenamento compartilhado do cluster está localizado em `/projetos`, montado via NFS em todos os nós. Cada projeto de pesquisa possui um diretório próprio, e dentro dele cada membro tem seu subdiretório pessoal:

```
/projetos/<nome-do-projeto>/<usuario>/
```

### Permissões

- Cada usuário possui permissão de **leitura e escrita** apenas em seu próprio diretório.
- Todos os membros de um mesmo projeto possuem permissão de **leitura** nos diretórios dos demais membros do grupo.
- Usuários de projetos diferentes **não** têm acesso entre si.

### Estrutura de diretórios

Embora não seja obrigatória, a seguinte estrutura de diretórios é recomendada para manter os projetos organizados:

```
/projetos/<projeto>/<usuario>/
├── src/            # Código-fonte dos programas
├── build/          # Executáveis compilados
├── input/          # Arquivos de entrada das simulações
├── output/         # Resultados e saídas dos jobs
├── jobs/           # Scripts de submissão Slurm (.sh)
└── logs/           # Arquivos de log gerados pelo Slurm
```

### Exemplo com dois projetos

Considere os projetos `hidro` (coordenado por `juliana.costa`) e `astro` (coordenado por `carlos.almeida`), cada um com seus membros:

```
/projetos/
├── hidro/
│   ├── juliana.costa/
│   │   ├── src/
│   │   ├── input/
│   │   └── output/
│   ├── rafael.mendes/
│   └── camila.torres/
└── astro/
    ├── carlos.almeida/
    │   ├── src/
    │   ├── input/
    │   └── output/
    ├── maria.souza/
    └── joao.pereira/
```

`rafael.mendes` pode ler os arquivos de `juliana.costa` e `camila.torres`, mas não tem acesso a nenhum diretório do projeto `astro`.

### Consultando seus projetos

No cluster, o comando `meus-projetos` lista os projetos aos quais seu usuário está vinculado:

```bash
$ meus-projetos
Usuário: rafael.mendes
Projetos:
  - hidro   →  /projetos/hidro/rafael.mendes
```

---

## Slurm — Submissão de Jobs

O **Slurm Workload Manager** é responsável por escalonar e executar os jobs no cluster. Todos os programas com consumo significativo de recursos devem ser submetidos via Slurm.

### Filas disponíveis

| Fila | Nós | Tempo máximo | Uso recomendado |
|---|---|---|---|
| `debug` | 1 | 30 minutos | Testes rápidos, verificação de compilação |
| `short` | 2 | 4 horas | Execuções curtas e interativas |
| `long` | 2 | 7 dias | Simulações de duração média |
| `max` | 2 | Ilimitado | Simulações longas (uso justificado) |

A fila padrão (quando não especificada) é `debug`.

### Comandos básicos do Slurm

```bash
# Submeter um job
sbatch job.sh

# Listar seus jobs na fila
squeue -u $USER

# Cancelar um job
scancel <job_id>

# Ver informações detalhadas sobre um job
scontrol show job <job_id>

# Ver status dos nós
sinfo
```

---

## Exemplos de Jobs

### Exemplo 1 — Job simples (teste)

Script básico para verificar que o ambiente está funcionando:

```bash
#!/bin/bash
#SBATCH --job-name=teste
#SBATCH --output=logs/teste_%j.out
#SBATCH --error=logs/teste_%j.err
#SBATCH --partition=debug
#SBATCH --ntasks=1
#SBATCH --time=00:05:00

echo "Hostname: $(hostname)"
echo "Data: $(date)"
echo "Diretório de trabalho: $(pwd)"
```

```bash
sbatch jobs/teste.sh
```

---

### Exemplo 2 — Job MPI (múltiplos processos em múltiplos nós)

Execução de um programa MPI distribuído entre os dois nós, utilizando 48 processos:

```bash
#!/bin/bash
#SBATCH --job-name=simulacao-mpi
#SBATCH --output=logs/mpi_%j.out
#SBATCH --error=logs/mpi_%j.err
#SBATCH --partition=long
#SBATCH --nodes=2
#SBATCH --ntasks-per-node=24
#SBATCH --time=12:00:00

# Carregar módulo MPI
module load openmpi

# Executar o programa com 48 processos (24 por nó)
srun ./build/meu_programa_mpi < input/parametros.dat
```

```bash
sbatch jobs/simulacao_mpi.sh
```

---

### Exemplo 3 — Job OpenMP (múltiplas threads em um nó)

Utilização de 32 threads OpenMP em um único nó para paralelismo de memória compartilhada:

```bash
#!/bin/bash
#SBATCH --job-name=simulacao-omp
#SBATCH --output=logs/omp_%j.out
#SBATCH --error=logs/omp_%j.err
#SBATCH --partition=short
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=32
#SBATCH --time=02:00:00

export OMP_NUM_THREADS=32

./build/meu_programa_openmp
```

```bash
sbatch jobs/simulacao_omp.sh
```

---

### Exemplo 4 — Job Híbrido MPI + OpenMP

Combinação de MPI entre nós e OpenMP dentro de cada nó — estratégia comum para programas de grande escala:

```bash
#!/bin/bash
#SBATCH --job-name=hibrido-mpi-omp
#SBATCH --output=logs/hibrido_%j.out
#SBATCH --error=logs/hibrido_%j.err
#SBATCH --partition=long
#SBATCH --nodes=2
#SBATCH --ntasks-per-node=4
#SBATCH --cpus-per-task=12
#SBATCH --time=24:00:00

module load openmpi

# 2 nós × 4 processos MPI × 12 threads OpenMP = 96 threads totais
export OMP_NUM_THREADS=12
srun ./build/programa_hibrido
```

---

### Exemplo 5 — Job PLUTO (simulação astrofísica/MHD)

Execução de uma simulação de magnetohidrodinâmica com o código PLUTO, distribuída entre os dois nós:

```bash
#!/bin/bash
#SBATCH --job-name=pluto-mhd
#SBATCH --output=logs/pluto_%j.out
#SBATCH --error=logs/pluto_%j.err
#SBATCH --partition=long
#SBATCH --nodes=2
#SBATCH --ntasks-per-node=16
#SBATCH --time=5-00:00:00

module load openmpi

# Entrar no diretório da simulação (onde estão pluto.ini e o executável)
cd /projetos/astro/joao.pereira/jet_simulation

# Executar o PLUTO com 32 processos MPI
srun ./pluto -x1 4 -x2 4 -x3 2
```

A flag `-x1 4 -x2 4 -x3 2` define a decomposição de domínio: 4 processos na direção X1, 4 em X2 e 2 em X3, totalizando 32 processos.

Após a execução, os arquivos de saída (`.dbl`, `.hdf5` ou `.vtk`) estarão no mesmo diretório e podem ser abertos com **ParaView** ou **VisIt** para visualização.

---

### Exemplo 6 — Array de jobs (varredura de parâmetros)

Útil para executar a mesma simulação com diferentes parâmetros de entrada, como varreduras de resolução ou condições iniciais:

```bash
#!/bin/bash
#SBATCH --job-name=sweep
#SBATCH --output=logs/sweep_%A_%a.out
#SBATCH --error=logs/sweep_%A_%a.err
#SBATCH --partition=short
#SBATCH --ntasks=8
#SBATCH --array=1-10
#SBATCH --time=04:00:00

module load openmpi

# Cada tarefa do array usa um arquivo de parâmetros diferente
PARAM_FILE="input/params_${SLURM_ARRAY_TASK_ID}.dat"

srun ./build/simulacao < $PARAM_FILE
```

```bash
sbatch jobs/sweep.sh
# Isso submeterá 10 jobs independentes (array IDs 1 a 10)
```
