# Log de Treino e Progressão

Planilha LibreOffice Calc para registro e progressão de treino, com bot Telegram para anotar pesos e RPE direto da academia — sem tocar no PC.

![Toguro](toguro.gif)

---

## Fluxo principal

```
Celular (Telegram)
  /gerar A          →  bot insere linhas no ODS, envia tabela com exercícios e pesos anteriores
  80 8              →  bot registra carga 80kg RPE 8 no exercício atual
  /status           →  mostra progresso da sessão
  /undo             →  desfaz último registro
```

O PC fica ligado com `python telegram_poller.py` rodando. O ODS é atualizado diretamente pelo Python, sem precisar abrir o LibreOffice.

---

## Arquivos

```
log-de-treino-e-progressao.ods   # LibreOffice Calc (arquivo principal)
GerarTreino.bas                  # Backup do macro Basic embutido no ODS
ods_ops.py                       # Manipulação direta do ODS via Python
telegram_poller.py               # Bot Telegram (polling)
.env                             # TELEGRAM_TOKEN=... (não versionado)
```

---

## Bot Telegram

### Iniciar

```bash
python telegram_poller.py
```

### Comandos

| Comando       | Descrição                                             |
| ------------- | ----------------------------------------------------- |
| `/gerar A`    | Gera treino A no ODS e envia tabela com pesos sugeridos |
| `/gerar B`    | Gera treino B                                         |
| `/gerar C`    | Gera treino C                                         |
| `80`          | Registra 80kg no próximo exercício pendente           |
| `80 8`        | Registra 80kg + RPE 8                                 |
| `/status`     | Mostra exercício atual e quantos foram concluídos     |
| `/undo`       | Desfaz último registro                                |
| `/help`       | Lista todos os comandos                               |

### Fallback (ODS aberto no LibreOffice)

Se o ODS estiver aberto quando você mandar o peso, o bot salva em `pending_log.csv`. Ao fechar o LibreOffice, clique em **Sincronizar** para aplicar os dados pendentes.

---

## Macro LibreOffice (alternativa ao bot)

A aba `TREINOS` tem botões **"Gerar Treino"** e **"Sincronizar"** que fazem o mesmo fluxo via interface gráfica.

**Gerar Treino:**
1. Clica no botão e digita `A`, `B` ou `C`
2. O macro insere as linhas, envia a tabela para o Telegram e gera o `session.json`

**Sincronizar:**
- Lê `pending_log.csv` e preenche `Carga_kg` e `RPE_final` nas linhas correspondentes

---

## O que o macro/bot preenche automaticamente

| Coluna           | Origem   | Descrição                                              |
| ---------------- | -------- | ------------------------------------------------------ |
| `Data`           | Macro    | Data do treino                                         |
| `Semana`         | Fórmula  | Semana ISO (`2026-W18`)                                |
| `Treino`         | Macro    | A, B ou C                                             |
| `Exercício`      | Macro    | Nome lido de EXERCICIOS                                |
| `Séries`         | Macro    | Séries planejadas                                      |
| `Reps`           | Macro    | Reps planejadas                                        |
| `Carga_kg`       | Bot/Manual | Carga utilizada em kg                                |
| `RPE_final`      | Bot/Manual | Percepção de esforço (6–10)                          |
| `Volume`         | Fórmula  | Séries × Reps × Carga_kg                              |
| `Decisão`        | Fórmula  | AUMENTAR / MANTER / REDUZIR                           |
| `Carga_anterior` | Fórmula  | Última carga registrada para o exercício               |
| `Próxima_carga`  | Fórmula  | Sugestão baseada na Decisão (±2,5 kg)                 |

**Lógica de Decisão:**
- RPE ≤ 8 → **AUMENTAR** (verde)
- RPE = 9 → **MANTER** (azul)
- RPE = 10 → **REDUZIR** (vermelho)

---

## Estrutura das Abas

| Aba          | Descrição                                                                  |
| ------------ | -------------------------------------------------------------------------- |
| `TREINOS`    | Registro de cada exercício com progressão automática                       |
| `EXERCICIOS` | Catálogo de exercícios por treino (A/B/C) com séries e reps planejadas     |
| `DIETA`      | Metas diárias, totais consolidados e log de refeições com macros e micros  |
| `ALIMENTOS`  | Tabela de referência nutricional dos alimentos cadastrados                 |

### Estrutura de `EXERCICIOS`

Sem cabeçalho. Colunas: `Exercicio | Series | Reps`

- Treino **A** — linhas 1–8 (Agachamento, Remada, Supino, Pull-over, Elev. lateral, Crucifixo inv., Rosca, Tríceps)
- Treino **B** — linhas 9–15 (Agachamento leve, Stiff, Desenvolvimento, Remada, Crucifixo inv., Supino, Elev. lateral leve)
- Treino **C** — linhas 16–18
