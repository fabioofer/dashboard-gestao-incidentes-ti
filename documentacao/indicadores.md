# Indicadores e Visualizações

## 1. Objetivo

Os indicadores foram desenvolvidos para transformar os registros operacionais em informações de fácil interpretação, permitindo analisar o volume de incidentes, sua distribuição e situações que podem exigir acompanhamento.

A solução combina indicadores consolidados, gráficos e tabelas de detalhamento.

---

# 2. Visão Geral

A página **Visão Geral** apresenta uma visão consolidada dos incidentes monitorados.

## 2.1 Incidentes totais

Apresenta a quantidade total de registros de incidentes presentes na base analisada.

**Medida:**

```DAX
Incidentes Total =
COUNTROWS ( F_Incidentes )
```

**Finalidade:** apresentar o volume geral de incidentes.

---

## 2.2 Incidentes do turno 19–07

Apresenta a quantidade de incidentes classificados como pertencentes ao turno das 19h às 07h.

**Medida:**

```DAX
Incidentes Turno 19–07 =
COALESCE(
    CALCULATE(
        COUNTROWS ( 'F_Incidentes' ),
        'F_Incidentes'[Turno_19_07] = 1
    ),
    0
)
```

**Finalidade:** permitir a análise específica das ocorrências relacionadas ao período de plantão.

---

## 2.3 Abertura > 2h

Apresenta a quantidade de ocorrências classificadas como `Operadora - Abertura` cujo tempo de indisponibilidade é superior a duas horas.

**Finalidade:** destacar ocorrências de abertura que ultrapassaram o limite definido para acompanhamento.

---

## 2.4 Unidades com 2 ou mais circuitos afetados

Apresenta a quantidade de unidades que possuem pelo menos duas designações distintas associadas a ocorrências de operadora.

**Finalidade:** sinalizar unidades que apresentam múltiplos circuitos afetados.

---

## 2.5 Incidentes por UF

Gráfico utilizado para apresentar a distribuição dos incidentes entre as Unidades Federativas.

A medida utilizada contabiliza os registros da tabela `F_Incidentes`, enquanto o campo UF é utilizado para agrupar os resultados.

**Finalidade:** permitir a análise da distribuição geográfica das ocorrências.

---

## 2.6 Incidentes por Operadora

Gráfico utilizado para apresentar a distribuição dos incidentes entre as operadoras.

A medida utilizada contabiliza os registros da tabela `F_Incidentes`, enquanto o campo Operadora é utilizado para agrupar os resultados.

**Finalidade:** permitir a análise da concentração das ocorrências entre diferentes operadoras.

---

## 2.7 Tabela Abertura > 2h

Apresenta o detalhamento das ocorrências que atendem ao critério de abertura superior a duas horas.

Entre as informações apresentadas estão:

- UF;
- CGC;
- Nome da Unidade;
- Designação;
- Operadora;
- Tipo de circuito;
- Tempo de indisponibilidade.

**Finalidade:** permitir identificar individualmente as ocorrências que compõem o indicador.

---

# 3. Detalhes

A página **Detalhes** permite aprofundar a análise das ocorrências.

## 3.1 Unidades com 2 links fora

Apresenta unidades que possuem duas ou mais designações distintas associadas a ocorrências de operadora, considerando a regra de exclusão de ocorrências de infraestrutura.

**Finalidade:** permitir identificar as unidades relacionadas ao indicador de múltiplos circuitos afetados.

---

## 3.2 Incidentes por UF

Apresenta a distribuição dos incidentes por Unidade Federativa.

**Finalidade:** permitir uma análise geográfica mais detalhada do conjunto de dados selecionado.

---

## 3.3 Incidentes por Operadora

Apresenta a distribuição dos incidentes por operadora.

**Finalidade:** permitir a análise das ocorrências de acordo com o provedor associado.

---

## 3.4 Detalhamento dos links privativos

Tabela destinada à análise detalhada dos circuitos privativos.

São apresentadas informações como:

- UF;
- Filial;
- CGC;
- Nome da Unidade;
- Operadora;
- Designação;
- Tipo de circuito;
- Problema;
- Tempo.

**Finalidade:** permitir a investigação individual dos registros relacionados aos links privativos.

---

# 4. Leituras Operacionais

A página **Leituras Operacionais** reúne indicadores e tabelas destinados à identificação de situações específicas dentro dos dados dos painéis Negocial e Tecnologia.

## 4.1 Total Negocial

Apresenta a quantidade de registros existentes na tabela `Negocial`.

**Finalidade:** apresentar a quantidade de unidades/ocorrências representadas no painel Negocial no contexto selecionado.

---

## 4.2 Causa Operadora

Apresenta a quantidade de unidades distintas classificadas com causa `OPERADORA` no painel Negocial.

**Finalidade:** identificar a quantidade de unidades cuja indisponibilidade está associada à classificação de operadora.

---

## 4.3 Causa Infraestrutura

Apresenta a quantidade de unidades distintas classificadas com causa `INFRAESTRUTURA` no painel Negocial.

**Finalidade:** identificar a quantidade de unidades cuja indisponibilidade está associada à infraestrutura.

---

## 4.4 Total AG/PAB/ADM

Apresenta a quantidade total de circuitos alarmados no painel Tecnologia, conforme o contexto de filtros aplicado.

**Finalidade:** fornecer uma visão consolidada da quantidade de circuitos alarmados.

---

## 4.5 Total Operadora

Apresenta a quantidade de incidentes classificados como `OPERADORA`.

**Finalidade:** identificar a parcela dos circuitos alarmados cuja classificação está relacionada à operadora.

---

## 4.6 Visita Agendada

Apresenta a quantidade de incidentes classificados como:

`Operadora - Visita Agendada`

**Finalidade:** acompanhar ocorrências em que a visita do provedor já possui informações de acesso e data disponibilizadas.

---

## 4.7 Previsão de Visita

Apresenta a quantidade de incidentes classificados como:

`Operadora - Previsão de Visita`

**Finalidade:** acompanhar ocorrências em que existe previsão de visita do provedor, mas que ainda não chegaram à condição de visita agendada.

---

## 4.8 Unidades com 2 ou mais links alarmados

Apresenta a quantidade de unidades que possuem duas ou mais designações distintas classificadas como `OPERADORA`.

**Finalidade:** identificar unidades que apresentam múltiplos circuitos associados a ocorrências de operadora.

---

## 4.9 Circuitos com mais de 100 horas

Apresenta a quantidade de incidentes cujo tempo de indisponibilidade é superior a 100 horas.

**Finalidade:** destacar ocorrências de longa duração.

---

## 4.10 Abertura > 2h

Apresenta as ocorrências classificadas como `Operadora - Abertura` com tempo superior a duas horas.

**Finalidade:** permitir o acompanhamento de ocorrências de abertura que ultrapassaram o limite definido.

---

## 4.11 Unidade com 1 circuito de Infraestrutura

Identifica unidades nas quais existe exatamente um circuito classificado como `Infraestrutura`.

**Finalidade:** sinalizar situações que podem demandar investigação operacional, especialmente quando outros circuitos da mesma unidade já apresentaram normalização.

---

# 5. Segmentadores

Todas as páginas do dashboard possuem seis segmentadores de dados:

- Data;
- UF;
- Operadora;
- Tipo de circuito;
- Problema;
- Filial.

Os segmentadores permitem alterar dinamicamente o contexto dos indicadores e das visualizações.

---

# 6. Relação entre as páginas

As três páginas possuem funções complementares:

```text
Visão Geral
     ↓
Identificação de situações relevantes
     ↓
Detalhes
     ↓
Investigação das ocorrências
     ↓
Leituras Operacionais
     ↓
Análise de situações específicas
```

A estrutura permite que a análise comece por indicadores consolidados e avance para informações mais detalhadas conforme a necessidade.

---

# 7. Apoio à tomada de decisão

Os indicadores não substituem a análise da equipe responsável pelo acompanhamento dos incidentes.

A função da solução é facilitar a interpretação dos dados e destacar situações que podem demandar investigação, acompanhamento ou escalonamento.

Dessa forma, o dashboard atua como uma ferramenta de apoio à análise operacional.
