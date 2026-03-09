# 🏋️ Log de Treino e Progressão

Planilha estruturada para registro, acompanhamento e análise da progressão de treino e nutrição. Organizada em múltiplas abas com separação clara entre dados brutos, dicionários de referência e análises.

---

## 📁 Estrutura do Arquivo

| Aba                      | Descrição                                                                 |
| ------------------------ | ------------------------------------------------------------------------- |
| `LOG_BRUTO`              | Registro detalhado de cada série realizada nos treinos                    |
| `DICIONARIO`             | Catálogo de exercícios por treino (A, B, C) com séries e reps planejadas  |
| `DICIONARIO RPE`         | Tabela de referência da escala RPE (Rate of Perceived Exertion)           |
| `ALIMENTACAO`            | Registro de refeições diárias com macros e calorias por alimento          |
| `RESUMO_DIARIO`          | Consolidado diário de macros com comparação às metas                      |
| `DICIONARIO ALIMENTACAO` | Tabela de referência nutricional dos alimentos cadastrados                |
| `PROGRESSAO`             | _(em construção)_ Análise de evolução de carga e volume ao longo do tempo |
| `DASHBOARD`              | _(em construção)_ Visão consolidada e indicadores de desempenho           |

---

## 📋 Schema das Abas

### `LOG_BRUTO`

Cada linha representa **uma série executada**.

| Coluna              | Tipo         | Descrição                                            |
| ------------------- | ------------ | ---------------------------------------------------- |
| `Data`              | Date         | Data do treino                                       |
| `Dia`               | String       | Identificador do treino (`A`, `B` ou `C`)            |
| `Sessao_ID`         | String       | ID único da sessão                                   |
| `Exercicio`         | String       | Nome do exercício                                    |
| `Serie`             | Integer      | Número da série                                      |
| `Reps`              | Integer      | Repetições realizadas                                |
| `Carga_kg`          | Float        | Carga utilizada em kg                                |
| `RPE`               | Integer      | Percepção de esforço (escala 6–10)                   |
| `RIR`               | Integer      | Repetições em reserva estimadas                      |
| `Volume`            | Float        | Volume da série (`Reps × Carga_kg`)                  |
| `Séries_planejadas` | Integer      | Número de séries previstas para o exercício          |
| `Progressão`        | String/Float | Indicador de progressão em relação à sessão anterior |

---

### `DICIONARIO`

Catálogo dos exercícios do programa, agrupados por treino.

| Coluna      | Descrição                         |
| ----------- | --------------------------------- |
| `Treino`    | Letra do treino (`A`, `B` ou `C`) |
| `Exercicio` | Nome completo do exercício        |
| `Series`    | Número de séries planejadas       |
| `Reps`      | Número de repetições planejadas   |

**Treinos:**

- **A** — Agachamento no Smith, Supino reto (pegada aberta), Puxada alta (triangular), Remada baixa (triangular), Desenvolvimento (pegada aberta), Rosca na polia barra reta (pegada supinada), Tríceps na polia barra reta
- **B** — Agachamento sumô, Stiff no Smith, Supino reto (pegada fechada), Puxada alta (pegada fechada), Desenvolvimento (pegada fechada), Rosca na polia com corda, Tríceps na polia com corda
- **C** — Agachamento frontal no Smith, Supino reto (pegada média), Remada alta no Smith, Puxada alta (pegada supinada), Remada baixa (pegada supinada), Rosca na polia (pegada pronada), Tríceps na polia (pegada supinada)

---

### `DICIONARIO RPE`

Tabela de referência para a escala de esforço percebido (RPE).

| RPE | Sensação          | RIR | Interpretação                                        |
| --- | ----------------- | --- | ---------------------------------------------------- |
| 6   | Leve              | 4+  | Série muito confortável, poderia fazer várias a mais |
| 7   | Moderado          | 3   | Ainda daria mais 3 repetições                        |
| 8   | Pesado controlado | 2   | Ainda daria mais 2 repetições                        |
| 9   | Muito pesado      | 1   | Só conseguiria mais 1 repetição                      |
| 10  | Falha             | 0   | Não conseguiria mais nenhuma repetição               |

> **RIR** = Reps in Reserve (repetições em reserva)

---

### `ALIMENTACAO`

Cada linha representa **um alimento em uma refeição**.

| Coluna         | Tipo   | Descrição                                          |
| -------------- | ------ | -------------------------------------------------- |
| `Data`         | Date   | Data da refeição                                   |
| `Refeição`     | String | Refeição do dia (ex: Almoço, Janta)                |
| `Alimento`     | String | Nome do alimento consumido                         |
| `Quantidade`   | Float  | Quantidade consumida                               |
| `Unidade_base` | String | Unidade de medida (`g`, `unidade`, etc.)           |
| `Peso_unit_g`  | Float  | Peso unitário em gramas (referência do dicionário) |
| `Proteína_g`   | Float  | Proteína total da porção (g)                       |
| `Carbo_g`      | Float  | Carboidrato total da porção (g)                    |
| `Gordura_g`    | Float  | Gordura total da porção (g)                        |
| `Calorias`     | Float  | Calorias totais da porção (kcal)                   |

---

### `RESUMO_DIARIO`

Cada linha representa **um dia**, com os macros totais consolidados a partir do `ALIMENTACAO`.

| Coluna               | Tipo  | Descrição                                            |
| -------------------- | ----- | ---------------------------------------------------- |
| `Data`               | Date  | Data do registro                                     |
| `Proteina_total`     | Float | Proteína total do dia (g)                            |
| `Carbo_total`        | Float | Carboidrato total do dia (g)                         |
| `Gordura_total`      | Float | Gordura total do dia (g)                             |
| `Calorias_total`     | Float | Calorias totais do dia (kcal)                        |
| `Peso_total_g`       | Float | Peso total de alimentos consumidos (g)               |
| `Densidade_calórica` | Float | Calorias por grama (`Calorias_total / Peso_total_g`) |

A aba também inclui uma tabela de referência lateral com as metas diárias de macros:

| Nutriente | Meta      | Faixa     |
| --------- | --------- | --------- |
| Proteína  | 200 g     | 180–220   |
| Carbo     | 200 g     | 170–220   |
| Gordura   | 70 g      | 60–80     |
| Calorias  | 2200 kcal | 2100–2300 |

---

### `DICIONARIO ALIMENTACAO`

Tabela de referência nutricional dos alimentos cadastrados no programa.

| Coluna           | Descrição                                       |
| ---------------- | ----------------------------------------------- |
| `Alimento`       | Nome do alimento                                |
| `Unidade`        | Unidade de medida padrão (`g`, `unidade`, etc.) |
| `Peso_unidade_g` | Peso da unidade em gramas                       |
| `Proteina_g`     | Proteína por unidade/100g (g)                   |
| `Carbo_g`        | Carboidrato por unidade/100g (g)                |
| `Gordura_g`      | Gordura por unidade/100g (g)                    |
| `Calorias`       | Calorias por unidade/100g (kcal)                |

---

## 🔄 Como Usar

1. **Registrar treinos** — Preencher `LOG_BRUTO` a cada sessão com os dados de cada série
2. **Registrar alimentação** — Preencher `ALIMENTACAO` com os alimentos consumidos em cada refeição
3. **Consultar o programa** — Usar `DICIONARIO` para conferir os exercícios, séries e reps planejados
4. **Calibrar esforço** — Usar `DICIONARIO RPE` para atribuir o RPE e RIR corretos em cada série
5. **Consultar macros** — Usar `RESUMO_DIARIO` para acompanhar o consumo diário vs. metas
6. **Acompanhar evolução** — _(futuro)_ Checar `PROGRESSAO` e `DASHBOARD` para análise da progressão

---

## 📌 Observações

- O campo `Volume` em `LOG_BRUTO` é calculado automaticamente como `Reps × Carga_kg`
- O campo `Progressão` compara a carga/volume atual com a sessão anterior do mesmo exercício
- Os macros em `ALIMENTACAO` são calculados com base no `DICIONARIO ALIMENTACAO` (quantidade × valor por unidade)
- As abas `PROGRESSAO` e `DASHBOARD` estão reservadas para análises futuras (pivot, gráficos, KPIs)
- O arquivo está disponível nos formatos `.xlsx` e `.ods` para compatibilidade com Excel e LibreOffice

---

## 🗂️ Formato dos Arquivos

```
log-de-treino-e-progressao.xlsx   # Microsoft Excel
log-de-treino-e-progressao.ods    # LibreOffice / Google Sheets
```
