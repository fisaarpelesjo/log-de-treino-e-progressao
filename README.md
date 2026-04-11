# 🏋️ Log de Treino e Progressão

Planilha estruturada para registro, acompanhamento e análise da progressão de treino e nutrição. Organizada em múltiplas abas com separação clara entre dados brutos, dicionários de referência e análise nutricional.

![Toguro](toguro.gif)

---

## 📁 Estrutura do Arquivo

| Aba          | Descrição                                                                 |
| ------------ | ------------------------------------------------------------------------- |
| `TREINOS`    | Registro de cada exercício realizado nos treinos com decisão de progressão |
| `EXERCICIOS` | Catálogo de exercícios por treino (A e B) com séries e reps planejadas    |
| `DIETA`      | Metas diárias, totais consolidados e log de refeições com macros e micros |
| `ALIMENTOS`  | Tabela de referência nutricional dos alimentos cadastrados                |

---

## 📋 Schema das Abas

### `TREINOS`

Cada linha representa **um exercício executado em uma sessão**.

| Coluna           | Tipo    | Descrição                                                  |
| ---------------- | ------- | ---------------------------------------------------------- |
| `Data`           | Date    | Data do treino                                             |
| `Semana`         | String  | Semana ISO do treino (ex: `2026-W15`)                      |
| `Treino`         | String  | Identificador do treino (`A` ou `B`)                       |
| `Exercício`      | String  | Nome do exercício                                          |
| `Séries`         | Integer | Número de séries realizadas                                |
| `Reps`           | Integer | Repetições realizadas por série                            |
| `Carga_kg`       | Float   | Carga utilizada em kg                                      |
| `RPE_final`      | Integer | Percepção de esforço na última série (escala 6–10)         |
| `Volume`         | Float   | Volume total do exercício (`Séries × Reps × Carga_kg`)     |
| `Decisão`        | String  | Recomendação de progressão (`AUMENTAR`, `MANTER`, `REDUZIR`) |
| `Carga_anterior` | Float   | Carga utilizada na sessão anterior do mesmo exercício      |
| `Próxima_carga`  | Float   | Carga recomendada para a próxima sessão                    |
| `Observações`    | String  | Notas livres sobre a execução                              |

**Lógica de `Decisão`:**

- **AUMENTAR** — RPE ≤ 8: carga foi confortável, incremento na próxima sessão
- **MANTER** — RPE = 9: esforço adequado, mantém a mesma carga
- **REDUZIR** — RPE = 10: falha ou limite máximo, reduz carga na próxima sessão

---

### `EXERCICIOS`

Catálogo dos exercícios do programa, agrupados por treino.

| Coluna      | Descrição                         |
| ----------- | --------------------------------- |
| `Exercicio` | Nome completo do exercício        |
| `Series`    | Número de séries planejadas       |
| `Reps`      | Número de repetições planejadas   |

**Treinos:**

- **A** — Agachamento (barra), Remada curvada (barra), Supino reto (barra), Pull-over (barra), Elevação lateral (halter), Crucifixo invertido, Rosca direta (barra/halter), Tríceps testa (barra/halter)
- **B** — Agachamento (barra, leve -10%), Stiff com barra, Desenvolvimento (barra em pé), Remada curvada (barra), Crucifixo invertido, Supino reto (barra), Elevação lateral (halter, leve -10%)

---

### `DIETA`

Aba com três seções dispostas verticalmente:

**1. Metas diárias** — linha de referência com os alvos nutricionais:

| Nutriente  | Meta      |
| ---------- | --------- |
| Proteína   | 200 g     |
| Carbo      | 200 g     |
| Gordura    | 70 g      |
| Calorias   | 2200 kcal |
| Fibra      | 30 g      |
| Ômega-3    | 1,5 g     |
| Potássio   | 4000 mg   |
| Magnésio   | 400 mg    |
| Zinco      | 13 mg     |
| Vitamina D | 1000 UI   |

**2. Totais do dia** — soma consolidada dos macros e micros do dia atual:

| Coluna               | Descrição                                            |
| -------------------- | ---------------------------------------------------- |
| `Densidade_calórica` | Calorias por grama (`Calorias_total / Peso_total_g`) |
| `Peso_total_g`       | Peso total de alimentos consumidos (g)               |
| `Proteina_total`     | Proteína total do dia (g)                            |
| `Carbo_total`        | Carboidrato total do dia (g)                         |
| `Gordura_total`      | Gordura total do dia (g)                             |
| `Calorias_total`     | Calorias totais do dia (kcal)                        |
| `Fibra_total`        | Fibra total do dia (g)                               |
| `Omega3_total`       | Ômega-3 total do dia (g)                             |
| `Potassio_total`     | Potássio total do dia (mg)                           |
| `Magnesio_total`     | Magnésio total do dia (mg)                           |
| `Zinco_total`        | Zinco total do dia (mg)                              |
| `VitaminaD_total`    | Vitamina D total do dia (UI)                         |

**3. Log de refeições** — cada linha representa **um alimento em uma refeição**:

| Coluna         | Tipo   | Descrição                                          |
| -------------- | ------ | -------------------------------------------------- |
| `Refeição`     | String | Refeição do dia (ex: Café, Lanche, Almoço, Janta)  |
| `Alimento`     | String | Nome do alimento consumido                         |
| `Quantidade`   | Float  | Quantidade consumida                               |
| `Unidade_base` | String | Unidade de medida (`g`, `unidade`, `copo`, etc.)   |
| `Peso_unit_g`  | Float  | Peso unitário em gramas (referência do dicionário) |
| `Proteína_g`   | Float  | Proteína total da porção (g)                       |
| `Carbo_g`      | Float  | Carboidrato total da porção (g)                    |
| `Gordura_g`    | Float  | Gordura total da porção (g)                        |
| `Calorias`     | Float  | Calorias totais da porção (kcal)                   |
| `Fibra_g`      | Float  | Fibra total da porção (g)                          |
| `Omega3_g`     | Float  | Ômega-3 total da porção (g)                        |
| `Potassio_mg`  | Float  | Potássio total da porção (mg)                      |
| `Magnesio_mg`  | Float  | Magnésio total da porção (mg)                      |
| `Zinco_mg`     | Float  | Zinco total da porção (mg)                         |
| `VitaminaD_UI` | Float  | Vitamina D total da porção (UI)                    |

> Os valores de macros e micros são calculados automaticamente a partir do `ALIMENTOS` (quantidade × valor por unidade).

---

### `ALIMENTOS`

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
| `Fibra_g`        | Fibra por unidade/100g (g)                      |
| `Omega3_g`       | Ômega-3 por unidade/100g (g)                    |
| `Potassio_mg`    | Potássio por unidade/100g (mg)                  |
| `Magnesio_mg`    | Magnésio por unidade/100g (mg)                  |
| `Zinco_mg`       | Zinco por unidade/100g (mg)                     |
| `VitaminaD_UI`   | Vitamina D por unidade/100g (UI)                |

---

## 🔄 Como Usar

1. **Registrar treinos** — Preencher `TREINOS` a cada sessão com os dados de cada exercício
2. **Consultar o programa** — Usar `EXERCICIOS` para conferir os exercícios, séries e reps planejados por treino
3. **Registrar alimentação** — Preencher o log de refeições em `DIETA` com os alimentos consumidos
4. **Acompanhar macros e micros** — Consultar os totais consolidados em `DIETA` e comparar às metas diárias
5. **Adicionar alimentos** — Cadastrar novos itens em `ALIMENTOS` para que os cálculos nutricionais funcionem corretamente

---

## 📌 Observações

- O campo `Volume` em `TREINOS` é calculado como `Séries × Reps × Carga_kg`
- O campo `Semana` em `TREINOS` segue o formato ISO `YYYY-Www` (ex: `2026-W15`)
- A `Decisão` de progressão é baseada no `RPE_final`: ≤ 8 → AUMENTAR, 9 → MANTER, 10 → REDUZIR
- Os macros e micros em `DIETA` são calculados com base em `ALIMENTOS` (quantidade × valor por unidade)
- A seção de totais em `DIETA` consolida automaticamente todos os alimentos registrados no dia

---

## 🗂️ Formato dos Arquivos

```
log-de-treino-e-progressao.xlsx   # Microsoft Excel
log-de-treino-e-progressao.ods    # LibreOffice / Google Sheets
```
