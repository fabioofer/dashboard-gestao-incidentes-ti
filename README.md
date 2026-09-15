# Dashboard de Gestão de Incidentes de TI

Solução de Business Intelligence desenvolvida para análise, monitoramento e apoio à gestão de incidentes de infraestrutura de TI.

## 📌 Sobre o projeto

Este projeto consiste no desenvolvimento de um dashboard utilizando Microsoft Power BI para transformar dados operacionais provenientes de painéis de monitoramento de um sistema ITSM em informações visuais e analíticas.

A solução foi desenvolvida a partir de uma necessidade operacional: facilitar a interpretação de uma grande quantidade de registros de incidentes e permitir a identificação de situações que podem demandar maior atenção da equipe.

O dashboard possibilita analisar os incidentes sob diferentes perspectivas, incluindo localização, operadora, tipo de circuito, problema, tempo de indisponibilidade e período de ocorrência.

---

## 🎯 Objetivo

Desenvolver uma solução de Business Intelligence capaz de organizar e visualizar dados de incidentes de infraestrutura de TI, facilitando a identificação de situações relevantes para o acompanhamento operacional e apoiando o planejamento das atividades da equipe.

---

## 🔎 Problema

Os dados disponibilizados pelos painéis de monitoramento são apresentados principalmente em formato tabular, dificultando a identificação rápida de padrões, concentrações de incidentes e ocorrências que podem exigir atenção.

Entre as situações observadas estão:

- unidades com múltiplos circuitos afetados;
- incidentes com elevado tempo de indisponibilidade;
- ocorrências de abertura que permanecem acima de duas horas;
- incidentes relacionados a operadoras;
- circuitos classificados como infraestrutura que permanecem como ocorrências isoladas;
- ocorrências em diferentes estágios de atendimento pelo provedor.

O dashboard busca facilitar a visualização dessas situações por meio de indicadores, filtros e detalhamento dos registros.

---

## 🏗️ Arquitetura da solução

O fluxo de dados utilizado no projeto é:

```text
Sistema ITSM
     │
     │ Exportação manual
     ▼
Arquivo Excel
     │
     ▼
Power Query
     │
     │ Tratamento e transformação
     ▼
Modelo de dados Power BI
     │
     │ Medidas e regras DAX
     ▼
Dashboard
```

### Fontes de dados

A solução utiliza informações provenientes de dois painéis operacionais do sistema ITSM:

- **Painel Negocial:** apresenta a perspectiva das unidades indisponíveis e suas respectivas causas.
- **Painel Tecnologia:** apresenta o detalhamento dos circuitos associados às ocorrências.

Os dados são exportados para Excel e posteriormente tratados no Power Query antes de serem utilizados no modelo do Power BI.

---

## 🧩 Modelo de dados

As principais estruturas utilizadas no modelo são:

### F_Incidentes

Tabela principal utilizada para análise dos registros provenientes do painel Tecnologia.

Entre os atributos utilizados estão:

- Unidade;
- CGC;
- UF;
- Filial;
- Designação;
- Operadora;
- Problema;
- Tipo de Problema;
- Tipo de Circuito;
- Tempo de indisponibilidade;
- Data;
- Turno.

### Negocial

Tabela utilizada para representar os dados do painel Negocial, com foco na identificação das unidades indisponíveis e na classificação das causas das ocorrências.

### D_Calendario

Dimensão temporal utilizada para organização e filtragem dos dados por:

- Ano;
- Mês;
- Dia;
- Dia da semana;
- Data.

### Dimensões auxiliares

O modelo também possui estruturas auxiliares relacionadas a:

- UF;
- Operadora;
- Unidade;
- Circuitos privativos.

---

## 📊 Estrutura do dashboard

O relatório é organizado em três páginas principais.

### 1. Visão Geral

Apresenta uma visão consolidada do cenário operacional.

Principais indicadores e análises:

- Incidentes totais;
- Incidentes do turno 19–07;
- Aberturas superiores a 2 horas;
- Unidades com dois ou mais circuitos afetados;
- Incidentes por UF;
- Incidentes por operadora;
- Detalhamento das ocorrências de abertura superiores a duas horas.

---

### 2. Detalhes

Permite aprofundar a análise dos registros e identificar as unidades e ocorrências relacionadas aos indicadores.

Principais análises:

- Unidades com dois ou mais circuitos associados a ocorrências de operadora;
- Incidentes por UF;
- Incidentes por operadora;
- Detalhamento dos links privativos.

---

### 3. Leituras Operacionais

Página destinada à análise de situações específicas identificadas a partir dos dados dos painéis Negocial e Tecnologia.

Entre as análises disponíveis estão:

- Total de unidades indisponíveis;
- Unidades classificadas por causa Operadora ou Infraestrutura;
- Total de circuitos alarmados;
- Total de circuitos classificados como Operadora;
- Ocorrências com visita agendada;
- Ocorrências com previsão de visita;
- Unidades com dois ou mais links classificados como Operadora;
- Circuitos com mais de 100 horas de indisponibilidade;
- Aberturas superiores a duas horas;
- Unidades com um único circuito classificado como Infraestrutura.

---

## 🧠 Principais regras de análise

A solução utiliza medidas DAX para aplicar regras de negócio aos dados.

### Abertura superior a 2 horas

São identificadas ocorrências que atendem simultaneamente aos critérios:

```text
Problema = "Operadora - Abertura"
Tempo de indisponibilidade > 2 horas
```

O objetivo é destacar ocorrências de abertura que permanecem acima do limite de duas horas.

### Múltiplos circuitos afetados

São identificadas unidades que possuem duas ou mais designações distintas associadas a ocorrências relacionadas à operadora.

Essa análise permite destacar unidades que apresentam múltiplos circuitos afetados.

### Circuitos com mais de 100 horas

São identificados registros cujo tempo de indisponibilidade é superior a 100 horas.

Essa informação permite direcionar a análise para ocorrências de longa duração.

### Previsão de visita x Visita agendada

O dashboard diferencia dois estágios do atendimento da operadora:

- **Previsão de visita:** o provedor informou que realizará uma visita, mas ainda não foram disponibilizadas as informações necessárias para o atendimento agendado.
- **Visita agendada:** as informações de acesso e a data da visita já foram disponibilizadas.

### Circuito único classificado como Infraestrutura

A solução também identifica unidades nas quais permanece um único circuito classificado como Infraestrutura.

Essa condição funciona como um sinal para investigação operacional, pois uma ocorrência remanescente pode necessitar de nova análise e eventual contato com o provedor.

---

## 🎛️ Filtros

As páginas do dashboard possuem segmentadores que permitem restringir dinamicamente a análise.

Os filtros disponíveis são:

- **Data**
- **UF**
- **Operadora**
- **Tipo de circuito**
- **Problema**
- **Filial**

A utilização dos filtros permite analisar diferentes recortes dos dados sem alterar a estrutura do relatório.

---

## 🛠️ Tecnologias utilizadas

- Microsoft Power BI
- Power Query
- DAX
- Microsoft Excel
- GitHub

---

## 🔄 Tratamento dos dados

O Power Query é utilizado para preparação dos dados antes da análise.

Entre as transformações presentes no processo estão:

- conversão e tratamento de campos;
- transformação de informações temporais;
- criação de campos derivados;
- aplicação de filtros;
- criação de colunas condicionais;
- reorganização e adequação da estrutura dos dados.

Após o tratamento, os dados são disponibilizados no modelo do Power BI para utilização das medidas e dos visuais.

---

## 📈 Apoio à análise operacional

O objetivo da solução não é substituir a análise da equipe, mas facilitar a identificação de situações relevantes dentro de um grande volume de registros.

A utilização de indicadores e detalhamentos permite partir de uma visão consolidada e chegar ao nível da ocorrência ou unidade que necessita de investigação.

Dessa forma, o dashboard transforma dados originalmente apresentados de forma predominantemente tabular em diferentes perspectivas de análise.

---

## ⚠️ Limitações

A solução atualmente depende da exportação manual dos dados do sistema ITSM para arquivos Excel.

Consequentemente, a atualização dos dados depende dessa etapa de obtenção da fonte.

Outra limitação é que os dados utilizados no ambiente original possuem caráter operacional e corporativo. Por esse motivo, informações que possam identificar unidades, circuitos, endereços, equipamentos ou outros elementos internos não são disponibilizadas neste repositório.

---

## 🔐 Dados e segurança

Este repositório tem finalidade de documentação e demonstração do projeto.

Dados corporativos, informações confidenciais, credenciais, endereços internos, identificadores de equipamentos e demais informações que possam comprometer a segurança ou a confidencialidade do ambiente de origem não devem ser publicados.

As imagens e materiais disponibilizados neste repositório devem ser previamente anonimizados quando necessário.

---

## 🚀 Possíveis evoluções

Entre as possibilidades de evolução da solução estão:

- integração direta entre o Power BI e a fonte de dados do ITSM;
- redução da dependência da exportação manual;
- automatização do processo de atualização;
- criação de novos indicadores;
- evolução das regras de priorização;
- utilização de análises históricas para identificação de padrões;
- ampliação das funcionalidades de apoio à tomada de decisão.

---

## 👤 Autoria

**Fábio William**

Projeto desenvolvido para estudo, desenvolvimento profissional e documentação de solução de Business Intelligence aplicada à gestão de incidentes de infraestrutura de TI.

---

## 📄 Observação

Este projeto é apresentado de forma anonimizada e não contém dados corporativos confidenciais da fonte original.
