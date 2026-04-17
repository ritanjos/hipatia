# Grupos de Pesquisa

!!! warning "Aviso"
    Os grupos de pesquisa listados nesta página são **fictícios** e foram criados apenas para fins ilustrativos da documentação. Qualquer semelhança com grupos reais é mera coincidência.

---

## Astrofísica Computacional e Plasmas (ACP)

**Responsável:** Prof. Dr. Carlos Henrique Almeida  
**Instituição:** Universidade Federal do Paraná — Campus Palotina  
**Departamento:** Departamento de Ciências Exatas e Tecnológicas  
**E-mail de contato:** `carlos.almeida@palotina.ufpr.br`

**Descrição:**  
O grupo ACP investiga fenômenos de plasma e fluidos astrofísicos por meio de simulações numéricas de magnetohidrodinâmica (MHD). As pesquisas atuais incluem a modelagem de jatos relativísticos, ventos estelares e instabilidades em discos de acreção ao redor de objetos compactos. O código PLUTO é a principal ferramenta computacional utilizada pelo grupo.

**Ferramentas utilizadas no cluster:** PLUTO (MHD), OpenMPI, ParaView

**Equipe:**

| Nome | Vínculo | Área de pesquisa |
|---|---|---|
| Prof. Dr. Carlos Henrique Almeida | Coordenador / Docente | Simulações MHD, jatos astrofísicos |
| Dra. Maria Souza | Pós-doutoranda | Instabilidades de Kelvin-Helmholtz |
| João Pereira | Doutorando | Ventos estelares e acreção |
| Fernanda Oliveira | Mestranda | Discos de acreção relativísticos |

---

## Grupo de Hidrodinâmica Computacional (GHC)

**Responsável:** Profa. Dra. Juliana Ribeiro Costa  
**Instituição:** Universidade Federal do Paraná — Campus Palotina  
**Departamento:** Departamento de Ciências Agrárias e Ambientais  
**E-mail de contato:** `juliana.costa@palotina.ufpr.br`

**Descrição:**  
O GHC aplica métodos computacionais para o estudo de escoamentos de fluidos em contextos ambientais e agrícolas. As pesquisas incluem simulações de escoamento em canais de irrigação, modelagem de transporte de sedimentos em bacias hidrográficas e análise de turbulência em sistemas fluviais. O grupo utiliza MPI para paralelização de seus solvers de volumes finitos desenvolvidos internamente.

**Ferramentas utilizadas no cluster:** OpenMPI, OpenMP, Python (NumPy/SciPy)

**Equipe:**

| Nome | Vínculo | Área de pesquisa |
|---|---|---|
| Profa. Dra. Juliana Ribeiro Costa | Coordenadora / Docente | Escoamentos turbulentos, irrigação |
| Rafael Mendes | Doutorando | Transporte de sedimentos |
| Camila Torres | Mestranda | Modelagem de bacias hidrográficas |
| Lucas Farias | Graduando (IC) | Escoamento em canal aberto |

---

## Laboratório de Modelagem Climática Regional (LMCR)

**Responsável:** Prof. Dr. André Luiz Veiga  
**Instituição:** Universidade Estadual do Oeste do Paraná — UNIOESTE (grupo colaborador)  
**E-mail de contato:** `andre.veiga@unioeste.br`

**Descrição:**  
O LMCR desenvolve simulações climáticas regionais para o Sul do Brasil, com ênfase em eventos extremos de precipitação e variabilidade climática sazonal. O grupo utiliza o modelo WRF (Weather Research and Forecasting) paralelizado via MPI, com rodadas que chegam a consumir vários dias de processamento na fila `long`.

**Ferramentas utilizadas no cluster:** OpenMPI, WRF, NCO, Python (xarray/matplotlib)

**Equipe:**

| Nome | Vínculo | Área de pesquisa |
|---|---|---|
| Prof. Dr. André Luiz Veiga | Coordenador / Docente | Modelagem climática regional |
| Beatriz Nascimento | Doutoranda | Eventos extremos de precipitação |
| Rodrigo Machado | Mestrando | Variabilidade do ENOS no Sul do Brasil |
