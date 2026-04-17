# Ferramentas

O cluster disponibiliza um conjunto de ferramentas voltadas à programação paralela, computação distribuída e simulação de fenômenos físicos. A seguir são descritas as principais ferramentas disponíveis.

---

## MPI — Message Passing Interface

**Implementação disponível:** OpenMPI

O MPI é o padrão de fato para programação paralela em ambientes de memória distribuída, como clusters. Ele permite que múltiplos processos, executando em diferentes nós, troquem dados entre si por meio de passagem de mensagens. No cluster, o OpenMPI está configurado para utilizar a interconexão Ethernet entre `node01` e `node02`.

### Características

- Suporte a comunicação ponto a ponto (`MPI_Send`, `MPI_Recv`) e coletiva (`MPI_Bcast`, `MPI_Reduce`, `MPI_Scatter`, `MPI_Gather`)
- Integração com Slurm via `srun` e `mpirun`
- Suporte a programas em C, C++ e Fortran
- Versão disponível: OpenMPI 4.x

### Compilando e executando um programa MPI

```bash
# Compilar um programa C com MPI
mpicc -o meu_programa meu_programa.c

# Compilar um programa Fortran com MPI
mpif90 -o meu_programa meu_programa.f90

# Executar com 8 processos (via Slurm)
srun --ntasks=8 ./meu_programa
```

---

## OpenMP — Open Multi-Processing

O OpenMP é uma API para programação paralela em memória compartilhada, baseada em diretivas de compilador (`#pragma omp`). É ideal para paralelizar laços e seções de código dentro de um único nó, aproveitando os 96 núcleos físicos (192 threads) disponíveis em cada servidor.

### Características

- Paralelismo baseado em threads (modelo fork-join)
- Suporte a C, C++ e Fortran
- Compatível com os compiladores GCC e Intel disponíveis no cluster
- Pode ser combinado com MPI para paralelismo híbrido (MPI entre nós + OpenMP dentro de cada nó)

### Compilando e executando um programa OpenMP

```bash
# Compilar com suporte a OpenMP (GCC)
gcc -fopenmp -o meu_programa meu_programa.c

# Definir o número de threads antes de executar
export OMP_NUM_THREADS=16
./meu_programa

# Dentro de um job Slurm, use --cpus-per-task para reservar threads
#SBATCH --cpus-per-task=16
```

### Exemplo de uso híbrido MPI + OpenMP

```bash
# 2 processos MPI, cada um com 16 threads OpenMP = 32 threads totais
#SBATCH --ntasks=2
#SBATCH --cpus-per-task=16

export OMP_NUM_THREADS=16
srun ./meu_programa_hibrido
```

---

## PLUTO — Modelagem Computacional de Fenômenos Físicos

O **PLUTO** é um código modular de alta performance para a simulação numérica de plasmas e fluidos astrofísicos, desenvolvido pela Universidade de Torino (Itália). Ele resolve as equações da hidrodinâmica (HD), magnetohidrodinâmica (MHD) e relatividade especial em geometrias cartesianas, cilíndricas e esféricas.

No cluster da UFPR Campus Palotina, o PLUTO é utilizado principalmente por grupos de pesquisa em astrofísica computacional, física de plasmas e dinâmica de fluidos.

### Características

- Suporte a múltiplos esquemas numéricos (Godunov, CTU, RK)
- Geometrias: cartesiana, cilíndrica, esférica
- Física suportada: HD, MHD, relatividade especial (RHD, RMHD)
- Paralelização via MPI (domínio distribuído entre processos)
- Saída em formatos HDF5, VTK e texto plano
- Compatível com visualização em VisIt e ParaView

### Estrutura de uma simulação PLUTO

Uma simulação típica com o PLUTO requer os seguintes arquivos no diretório de trabalho:

```
minha_simulacao/
├── pluto.ini          # Parâmetros da simulação (resolução, tempo, saída)
├── definitions.h      # Configurações de física e geometria
├── init.c             # Condições iniciais do problema
├── Makefile           # Gerado pelo script de configuração
└── pluto              # Executável compilado
```

### Configurando e compilando o PLUTO

```bash
# Entrar no diretório da simulação
cd /projetos/astro/joao.silva/minha_simulacao

# Configurar o PLUTO (modo interativo)
python $PLUTO_DIR/setup.py

# Compilar
make

# Submeter ao Slurm (veja exemplos em "Como Utilizar")
sbatch job_pluto.sh
```

### Saídas e visualização

O PLUTO grava arquivos de saída numérica em intervalos definidos no `pluto.ini`. Os formatos VTK e HDF5 podem ser abertos diretamente no **ParaView** ou **VisIt** para visualização 2D e 3D dos campos físicos (densidade, velocidade, pressão, campo magnético, etc.).

---

## Slurm — Gerenciador de Jobs

O **Slurm Workload Manager** é o sistema de escalonamento de jobs do cluster. Todos os programas que consomem recursos significativos de CPU ou memória devem ser submetidos via Slurm — nunca executados diretamente no nó mestre.

Para detalhes sobre filas, scripts de submissão e exemplos práticos, consulte a seção [Como utilizar](como-utilizar.md).
