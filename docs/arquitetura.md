# Arquitetura

O cluster HPC (*High Performance Computing*) da UFPR Campus Palotina é composto por **dois nós interligados via rede Gigabit Ethernet**, formando um ambiente de processamento paralelo e distribuído voltado à pesquisa científica e ao ensino.

## Visão Geral

```
                        ┌──────────────────────────────────┐
                        │          Rede Gigabit Ethernet   │
                        │           (1 GbE / IEEE 802.3)   │
                        └──────────┬──────────────┬────────┘
                                   │              │
                    ┌──────────────▼──┐      ┌────▼───────────────┐
                    │    node01       │      │    node02          │
                    │  (Nó Mestre)    │      │ (Nó de Computação) │
                    └─────────────────┘      └────────────────────┘
```

Os dois nós montam o mesmo sistema de arquivos compartilhado (`/projetos`) via NFS, garantindo que dados submetidos no nó mestre estejam imediatamente disponíveis para execução no nó de computação.

---

## Especificações dos Nós

Ambos os nós possuem configuração de hardware idêntica, baseada no servidor **Dell PowerEdge R7625**.

### node01 — Nó Mestre

| Componente | Especificação |
|---|---|
| **Modelo** | Dell PowerEdge R7625 |
| **Processador** | 2× AMD EPYC 9454 (2.75 GHz, 48 cores / 96 threads, 256 MB de cache L3, TDP 290 W) |
| **Total de núcleos** | 96 núcleos físicos / 192 threads |
| **Memória RAM** | 2× 16 GB RDIMM DDR5-4800 (32 GB total) |
| **Armazenamento** | 1× SSD SATA 480 GB (Read Intensive, 6 Gbps, hot-plug) |
<!-- | **Rede** | Broadcom 5720 Dual Port 1 GbE LOM | -->
<!-- | **Controladora RAID** | Front H355 (PERC 11) | -->

**Papel no cluster:** gerenciamento do ambiente Slurm, execução de jobs submetidos pelo Slurm, autenticação de usuários, exportação NFS do diretório `/projetos`, ponto de acesso SSH externo.

---

### node02 — Nó de Computação

| Componente | Especificação |
|---|---|
| **Modelo** | Dell PowerEdge R7625 |
| **Processador** | 2× AMD EPYC 9454 (2.75 GHz, 48 cores / 96 threads, 256 MB de cache L3, TDP 290 W) |
| **Total de núcleos** | 96 núcleos físicos / 192 threads |
| **Memória RAM** | 2× 16 GB RDIMM DDR5-4800 (32 GB total) |
| **Armazenamento** | 1× SSD SATA 480 GB (Read Intensive, 6 Gbps, hot-plug) |
| **Rede** | Broadcom 5720 Dual Port 1 GbE LOM |
<!-- | **Controladora RAID** | Front H355 (PERC 11) | -->
<!-- | **Fonte de alimentação** | Dual hot-plug redundante 1+1 (1400 W, Mixed Mode) | -->

**Papel no cluster:** execução dos jobs submetidos pelo Slurm, montagem do `/projetos` via NFS.

---

## Capacidade total do cluster

| Recurso | Valor |
|---|---|
| Nós de computação | 2 |
| Núcleos físicos totais | 192 (2 × 96) |
| Threads totais | 384 (2 × 192) |
| Memória RAM total | 64 GB (2 × 32 GB) |
| Armazenamento total (SSDs locais) | 960 GB (2 × 480 GB) |
| Interconexão | Gigabit Ethernet (1 GbE) |

