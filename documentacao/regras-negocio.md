# Regras de Negócio e Critérios de Análise

## 1. Objetivo

O dashboard utiliza regras de análise para transformar os registros operacionais em indicadores capazes de destacar situações que podem demandar atenção da equipe.

As regras foram definidas a partir das necessidades observadas durante o acompanhamento dos painéis de monitoramento e posteriormente implementadas no Power BI por meio de medidas e campos calculados.

---

## 2. Abertura superior a 2 horas

### Critério

Uma ocorrência é considerada para este indicador quando atende simultaneamente aos seguintes critérios:

- Problema igual a `Operadora - Abertura`;
- Tempo de indisponibilidade superior a 2 horas.

### Finalidade

Identificar ocorrências de abertura que permanecem por período superior a duas horas, permitindo seu acompanhamento e eventual escalonamento operacional.

---

## 3. Unidades com dois ou mais circuitos afetados

### Critério

Uma unidade é sinalizada quando possui duas ou mais designações distintas associadas a ocorrências relacionadas à operadora.

A análise considera a quantidade distinta de `Designação` dentro do contexto da unidade.

### Finalidade

Identificar unidades que apresentam múltiplos circuitos afetados por ocorrências de operadora, possibilitando direcionar a atenção para situações potencialmente mais relevantes para a conectividade da unidade.

---

## 4. Exclusão de ocorrências de infraestrutura na análise de múltiplos circuitos

Em determinadas análises de múltiplos circuitos, são consideradas ocorrências relacionadas à operadora e excluídos registros classificados como infraestrutura.

Essa diferenciação evita que ocorrências de naturezas distintas sejam tratadas da mesma forma durante a análise.

### Finalidade

Separar situações relacionadas ao provedor de situações classificadas como problemas de infraestrutura, permitindo uma leitura mais específica dos circuitos associados às ocorrências de operadora.

---

## 5. Circuitos com mais de 100 horas de indisponibilidade

### Critério

São identificados registros cujo tempo de indisponibilidade seja superior a 100 horas.

### Finalidade

Destacar ocorrências de longa duração para facilitar a identificação e o acompanhamento de circuitos que permanecem indisponíveis por períodos elevados.

---

## 6. Previsão de visita

### Critério

São contabilizados os incidentes classificados como:

`Operadora - Previsão de Visita`

### Interpretação operacional

Representa ocorrências em que o provedor informou que realizará uma visita à unidade, mas ainda não foram disponibilizadas as informações necessárias para o atendimento agendado.

### Finalidade

Permitir o acompanhamento das ocorrências que possuem previsão de atendimento, mas ainda não chegaram à etapa de visita efetivamente agendada.

---

## 7. Visita agendada

### Critério

São contabilizados os incidentes classificados como:

`Operadora - Visita Agendada`

### Interpretação operacional

Representa ocorrências em que os dados de acesso e a data da visita já foram disponibilizados pelo provedor.

### Finalidade

Permitir o acompanhamento dos incidentes que já possuem atendimento programado.

---

## 8. Unidades com dois ou mais links alarmados no painel Tecnologia

### Critério

Para cada unidade, é contabilizada a quantidade distinta de designações classificadas como `OPERADORA`.

São consideradas unidades que apresentam:

`Quantidade de links classificados como Operadora >= 2`

### Finalidade

Relacionar a visão de unidade indisponível apresentada pelo painel Negocial com o detalhamento dos circuitos apresentado pelo painel Tecnologia.

---

## 9. Unidade com um único circuito classificado como Infraestrutura

### Critério

A unidade é sinalizada quando apresenta exatamente uma designação distinta classificada como `Infraestrutura`.

### Interpretação operacional

Essa condição é utilizada como um sinal para investigação. Quando outros circuitos da mesma unidade deixam de apresentar a condição de indisponibilidade e permanece apenas uma ocorrência, essa ocorrência pode demandar nova análise para verificar se deve permanecer classificada como infraestrutura ou se necessita de investigação junto ao provedor.

### Finalidade

Evitar que ocorrências remanescentes permaneçam sem acompanhamento após a estabilização dos demais circuitos da unidade.

---

## 10. Análise por unidade

As regras relacionadas a múltiplos circuitos utilizam informações de identificação da unidade, como:

- CGC;
- Nome da Unidade;
- UF;
- Filial.

Essa abordagem permite que os incidentes sejam analisados não apenas individualmente, mas também considerando o conjunto de circuitos associados à mesma unidade.

---

## 11. Análise temporal

O dashboard utiliza informações temporais para permitir diferentes perspectivas de acompanhamento, incluindo:

- data da ocorrência;
- tempo de indisponibilidade;
- período de plantão;
- classificação do turno 19–07;
- análise por ano, mês, dia e dia da semana.

---

## 12. Filtros de análise

As regras e indicadores podem ser analisados de acordo com os seguintes segmentadores:

- Data;
- UF;
- Operadora;
- Tipo de circuito;
- Problema;
- Filial.

A aplicação dos filtros permite restringir o contexto dos indicadores e realizar análises específicas de acordo com a necessidade operacional.

---

## 13. Princípio de apoio à decisão

Os indicadores apresentados no dashboard não substituem a análise da equipe responsável pelo acompanhamento dos incidentes.

As regras funcionam como mecanismos de sinalização, permitindo destacar situações que podem exigir investigação, acompanhamento ou escalonamento.

O objetivo da solução é reduzir a dificuldade de interpretação de grandes volumes de registros e facilitar a identificação das ocorrências relevantes para o contexto operacional.
