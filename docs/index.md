# Hipatia

Bem-vindo à documentação oficial do **Hipatia**, o cluster do **Hub Integrado de Processamento Avançado e Tecnologias para Inovação em Astrofísica** da Universidade Federal do Paraná (UFPR) - Campus Palotina.

Esta plataforma é um recurso institucional dedicado à pesquisa científica, ao ensino e ao desenvolvimento de projetos que demandam processamento computacional intensivo.

## O que você encontra aqui

- [**Sobre**](sobre.md) — histórico, arquitetura e finalidade do cluster
- [**Arquitetura**](arquitetura.md) — especificações técnicas detalhadas dos nós
- [**Ferramentas**](ferramentas.md) — MPI, OpenMP, PLUTO e demais softwares disponíveis
- [**Como utilizar**](como-utilizar.md) — organização de diretórios, Slurm e exemplos práticos
- [**Solicitar Acesso**](solicitar-acesso.md) — procedimento para cadastro de projetos e usuários
- [**Grupos de Pesquisa**](grupos-pesquisa.md) — grupos que utilizam a infraestrutura
- [**Publicações**](publicacoes.md) — trabalhos produzidos com o apoio do cluster

## Início rápido

```bash
# Acesso via SSH, com instruções (após cadastro)
ssh usuario@hpc.palotina.ufpr.br

# Consultar seus projetos
permissoes

# Submeter um job de teste
sbatch meu_job.sh

# Acompanhar a fila
squeue -u $USER
```

## Suporte

Em caso de dúvidas técnicas ou problemas de acesso, entre em contato com a equipe de administração:

**E-mail:** `hpc-admin@palotina.ufpr.br`
