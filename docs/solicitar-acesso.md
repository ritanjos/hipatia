# Solicitar Acesso ao Cluster

O acesso ao Cluster HPC da UFPR Campus Palotina é concedido a pesquisadores, professores, alunos de graduação e pós-graduação vinculados a projetos de pesquisa ativos. Todo usuário deve estar associado a um projeto cadastrado e ter sua solicitação aprovada pelo responsável técnico do cluster.

---

## Requisitos para acesso

Para obter acesso ao cluster, é necessário que:

1. O solicitante esteja vinculado a uma instituição de ensino ou pesquisa (UFPR ou instituição parceira);
2. Exista um projeto de pesquisa ativo ao qual o solicitante será associado;
3. O coordenador do projeto assuma a responsabilidade pelo uso adequado dos recursos por parte de seus membros;
4. O solicitante concorde com a [Política de Uso Aceitável](#política-de-uso-aceitável) do cluster.

---

## Procedimento de solicitação

### 1. Cadastro de novo projeto

Caso o projeto ainda não esteja cadastrado no cluster, o **coordenador responsável** deve encaminhar uma solicitação por e-mail para a equipe de administração:

**E-mail:** `hpc-admin@palotina.ufpr.br`  
**Assunto:** `Solicitação de cadastro de projeto — Cluster HPC`

Utilize o modelo abaixo:

```
Assunto: Solicitação de cadastro de projeto — Cluster HPC

Prezados,

Solicito o cadastro do seguinte projeto de pesquisa no Cluster HPC
da UFPR Campus Palotina:

Nome do projeto: <nome curto, sem espaços, ex: hidro2024>
Título completo: <título do projeto de pesquisa>
Descrição breve: <descrição do objetivo computacional do projeto,
                  incluindo ferramentas previstas: MPI, OpenMP, PLUTO, etc.>
Área do conhecimento: <ex: Astrofísica, Hidrodinâmica, Bioinformática>
Previsão de término: <mês/ano>

Coordenador responsável:
  Nome: <nome completo>
  E-mail institucional: <e-mail>
  CPF: <CPF>
  Instituição: <nome da instituição>
  Departamento/Laboratório: <departamento ou laboratório>

Membros iniciais do projeto:
  1. Nome: <nome completo>
     E-mail: <e-mail>
     Vínculo: <graduação / mestrado / doutorado / pesquisador / professor>
     Instituição: <instituição>

  2. Nome: <nome completo>
     E-mail: <e-mail>
     Vínculo: <vínculo>
     Instituição: <instituição>

Atenciosamente,
<assinatura>
```

### 2. Inclusão de novo membro em projeto existente

Se o projeto já estiver cadastrado, o coordenador do projeto pode solicitar a inclusão de novos membros enviando e-mail para `hpc-admin@palotina.ufpr.br` com o assunto `Inclusão de membro — <nome do projeto>`, informando:

- Nome completo do novo membro
- E-mail institucional
- Vínculo (graduação, mestrado, doutorado, pesquisador, professor)
- Instituição de origem

---

## Após a aprovação

Após a análise e aprovação da solicitação pela equipe de administração:

- O coordenador receberá uma confirmação por e-mail;
- Cada membro cadastrado receberá, individualmente, um e-mail com:
    - seu nome de usuário no cluster;
    - instruções para definição de senha no primeiro acesso;
    - orientações de conexão via SSH;
    - link para esta documentação.

O prazo médio para resposta é de **até 5 dias úteis** após o recebimento da solicitação completa.

---

## Política de Uso Aceitável

O uso do Cluster HPC da UFPR Campus Palotina está condicionado ao cumprimento das seguintes diretrizes:

- Os recursos computacionais devem ser utilizados exclusivamente para atividades de pesquisa, ensino e extensão vinculadas ao projeto cadastrado;
- É vedada a execução de processos fora do gerenciador Slurm (exceto compilação e testes breves na fila `debug`);
- O usuário é responsável pelo armazenamento e backup de seus dados no diretório `/projetos`;
- É proibida a utilização do cluster para mineração de criptomoedas, atividades comerciais ou qualquer finalidade não acadêmica;
- O compartilhamento de credenciais de acesso é estritamente proibido;
- A equipe de administração reserva-se o direito de suspender contas em caso de uso indevido dos recursos.

Dúvidas sobre a política de uso podem ser enviadas para `hpc-admin@palotina.ufpr.br`.
