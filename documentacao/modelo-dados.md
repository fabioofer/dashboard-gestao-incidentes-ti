# Modelo de Dados

## 1. Visão geral

O modelo de dados foi estruturado no Microsoft Power BI para organizar as informações provenientes dos painéis operacionais do sistema ITSM e permitir sua análise por diferentes perspectivas.

A solução utiliza duas principais tabelas de dados operacionais:

- `F_Incidentes`;
- `Negocial`.

Além delas, são utilizadas dimensões e estruturas auxiliares para apoiar a análise.

---

## 2. Fluxo dos dados

O processo utilizado no projeto segue o fluxo:

```text
Sistema ITSM
     │
     ▼
Exportação para Excel
     │
     ▼
Power Query
     │
     ▼
Tratamento e transformação
     │
     ▼
Modelo de dados Power BI
     │
     ▼
Medidas DAX
     │
     ▼
Visualizações e indicadores
```

A obtenção dos dados é realizada por meio da exportação manual das informações do sistema ITSM para arquivos Excel.

---

## 3. Tabela F_Incidentes

A tabela `F_Incidentes` representa os dados utilizados na análise do painel Tecnologia.

Entre as principais informações utilizadas estão:

- identificação da unidade;
- CGC;
- UF;
- filial;
- designação do circuito;
- operadora;
- problema;
- tipo de problema;
- tipo de circuito;
- tempo de indisponibilidade;
- data da ocorrência;
- turno.

A tabela constitui a principal fonte para os indicadores relacionados aos circuitos e incidentes apresentados no dashboard.

---

## 4. Tabela Negocial

A tabela `Negocial` representa os dados utilizados na análise do painel Negocial.

Sua principal função é permitir a análise das unidades indisponíveis e de suas respectivas classificações.

Entre as informações utilizadas estão:

- CGC;
- unidade;
- filial;
- UF;
- operadora;
- problema;
- tipo de problema;
- designação;
- data;
- tempo.

A tabela é utilizada, entre outros objetivos, para identificar a quantidade de unidades classificadas como Operadora ou Infraestrutura.

---

## 5. Dimensão D_Calendario

A tabela `D_Calendario` funciona como dimensão temporal do modelo.

Possui atributos relacionados a:

- Ano;
- Data;
- Dia;
- Dia da semana;
- Número do mês;
- Nome do mês;
- Nome do dia da semana.

A dimensão é utilizada para organizar e filtrar os dados temporalmente.

---

## 6. Relacionamentos temporais

As tabelas `F_Incidentes` e `Negocial` possuem relacionamento com `D_Calendario` utilizando o campo `Data_Plantao`.

De forma simplificada:

```text
F_Incidentes
     │
     │ Data_Plantao
     ▼
D_Calendario

Negocial
     │
     │ Data_Plantao
     ▼
D_Calendario
```

Essa estrutura permite que os dados das duas fontes operacionais sejam analisados de acordo com o mesmo contexto temporal.

---

## 7. Dimensões auxiliares

O modelo também possui estruturas auxiliares para organização e análise dos dados:

### Dim_UF

Contém informações de Unidade Federativa utilizadas para análise e segmentação geográfica.

### Dim_Operadora

Contém informações relacionadas às operadoras utilizadas no modelo.

### Dim_Unidade

Concentra informações de identificação das unidades, incluindo:

- CGC;
- filial;
- nome da unidade;
- UF.

Essas estruturas auxiliam na organização dos dados e na construção das análises.

---

## 8. Estruturas relacionadas a circuitos privativos

O modelo possui estruturas auxiliares relacionadas à identificação e análise de unidades que apresentam múltiplos circuitos privativos.

Essas estruturas permitem apoiar análises específicas relacionadas aos circuitos e às unidades correspondentes.

---

## 9. Power Query

O Power Query é utilizado na etapa de preparação dos dados.

O processo inclui transformações como:

- conversão de tipos de dados;
- tratamento de informações;
- criação de campos derivados;
- aplicação de filtros;
- criação de colunas condicionais;
- reorganização da estrutura dos dados.

Essa etapa prepara os dados para utilização no modelo do Power BI.

---

## 10. Medidas DAX

Após a preparação dos dados, são utilizadas medidas e campos calculados em DAX para implementar os indicadores e regras de análise.

Entre os critérios implementados estão:

- quantidade total de incidentes;
- incidentes do turno 19–07;
- ocorrências de abertura superiores a duas horas;
- unidades com múltiplos circuitos afetados;
- circuitos com mais de 100 horas de indisponibilidade;
- ocorrências com previsão ou agendamento de visita;
- identificação de unidades com circuito único classificado como infraestrutura.

---

## 11. Segmentação dos dados

O modelo é utilizado nas páginas do dashboard em conjunto com seis segmentadores principais:

- Data;
- UF;
- Operadora;
- Tipo de circuito;
- Problema;
- Filial.

Os filtros permitem alterar o contexto de análise dos indicadores e das visualizações.

---

## 12. Relação entre os dados e o dashboard

A estrutura do modelo permite combinar diferentes níveis de informação:

```text
Painel Negocial
      │
      └── Unidades indisponíveis
                │
                ▼
        Classificação da causa

Painel Tecnologia
      │
      └── Circuitos e incidentes
                │
                ▼
       Problema / Operadora /
       Tempo / Tipo de circuito

                ↓

         Medidas e regras DAX

                ↓

       ┌──────────────────┐
       │   Visão Geral    │
       ├──────────────────┤
       │     Detalhes     │
       ├──────────────────┤
       │Leituras Operac.  │
       └──────────────────┘
```

Essa estrutura permite que informações apresentadas originalmente em diferentes perspectivas sejam analisadas de forma integrada no dashboard.

---

## 13. Limitação de reprodução

A solução depende atualmente da exportação dos dados do sistema ITSM para arquivos Excel.

Os arquivos de origem utilizados no ambiente operacional não são disponibilizados neste repositório devido ao caráter corporativo das informações.

Consequentemente, o repositório apresenta a documentação, as regras de negócio e as visualizações anonimizadas do projeto, mas não disponibiliza os dados operacionais originais.
