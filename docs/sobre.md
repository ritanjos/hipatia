# Sobre o Cluster

O **Hipatia** é o **Cluster HPC** (*High Performance Computing*) da UFPR Campus Palotina, e é uma infraestrutura de computação de alto desempenho dedicada ao apoio à pesquisa científica, ao ensino de graduação e pós-graduação e ao desenvolvimento de projetos computacionalmente intensivos.


## Por que um cluster de alto desempenho?

A pesquisa científica moderna enfrenta desafios que demandam capacidade computacional muito além do que estações de trabalho convencionais podem oferecer. Simulações de dinâmica de fluidos, modelagem de fenômenos astrofísicos, análises genômicas e estudos de sistemas complexos exigem a execução simultânea de milhares de processos, processamento de grandes volumes de dados e tempos de resposta compatíveis com os ritmos da produção científica.

O cluster HPC da UFPR Campus Palotina foi concebido para suprir exatamente essa demanda. Ao reunir servidores de alto desempenho interligados em rede de alta velocidade, ele oferece aos pesquisadores da instituição — e aos grupos colaboradores — uma plataforma capaz de executar simulações e análises que seriam inviáveis em hardware convencional, **democratizando o acesso ao processamento paralelo** e elevando a qualidade e o alcance da produção científica local.

## Arquitetura

O cluster é organizado nos seguintes componentes:

- **Nó mestre (`node01`)**  
  Responsável pelo gerenciamento do ambiente, autenticação de usuários, escalonamento de jobs via Slurm e acesso externo via SSH. Os usuários submetem seus trabalhos a partir deste nó.

- **Nó de computação (`node02`)**  
  Executa as tarefas submetidas pelo nó mestre. Possui os recursos de CPU, memória e armazenamento local necessários para as cargas de trabalho científicas.

- **Armazenamento compartilhado**  
  O diretório `/projetos` é montado via NFS e acessível por todos os nós, garantindo que os dados de entrada e saída dos jobs estejam disponíveis em qualquer ponto do cluster.

## Tecnologias utilizadas

- **Sistema Operacional:** Linux (Rocky Linux 9)
- **Gerenciador de jobs:** Slurm Workload Manager
- **Computação paralela:** OpenMPI, OpenMP
- **Modelagem computacional:** PLUTO (MHD/HD)
- **Acesso remoto:** SSH
- **Armazenamento compartilhado:** NFS

## Finalidade

O cluster é destinado a atividades de:

- pesquisa científica em diversas áreas do conhecimento
- ensino de computação científica e programação paralela
- desenvolvimento e validação de modelos computacionais
- processamento de cargas intensivas que demandem múltiplos núcleos ou nós
