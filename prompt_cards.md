# Prompt cards (copy and paste)

Replace the text in [square brackets]. Attach a file where the card says so, or paste its text between the tags.

---

## Activity 1 · Card 1 (RTCO, fill in the blanks)

```
Role: You are [who should answer?]
Task: Do not answer the question yet. List the [number] questions a briefing on "[topic]" must answer, and the data needed for each.
Context: [which reports? which dates? which definitions?]
Output: one table: question | data needed | source. Max [n] rows, [n] words per cell.
Guardrail: Do not state any forecast number. If unsure, write "To verify".
```

## Activity 1 · Card 1M (meta-prompt)

```
I am preparing a CEO briefing on why OPEC, the IEA and the EIA disagree about world oil demand in 2026.
Ask me up to 5 questions, one at a time.
Then write a prompt with Role, Task, Context, Output contract and Guardrails that makes a chatbot produce the PLAN of this briefing (the questions it must answer and the data needed), not the answer.
```

---

## Activity 2 · Card 2 (question 1)

Attach: `2026-09_IEF_comparison.pdf`

```
Role: oil-market data analyst. Use ONLY the attached IEF comparison of the September 2026 reports.
1. Quote the rows and sentences that give world oil demand for 2025, 2026 and each quarter of 2026.
2. From the quotes only, fill one table: agency | 2025 | 1Q26 | 2Q26 | 3Q26 | 4Q26 | 2026 | 2026 growth.
3. OPEC minus IEA: the gap in the 2026 level, in 2026 growth and in 2025. Show each subtraction. Does the 2025 gap plus the growth gap equal the level gap? If not, why?
4. For each quarter of 2026: highest minus lowest agency. Does it match the report's text?
If a number is not in the report, write "VERIFY -- not in source". No other text.
```

---

## Activity 3 · Card 3 (questions 2 and 3)

Attach: `2026-02_IEF_comparison.pdf`. Paste your table from question 1 and the text of `gdp_note.md`.

```
Role: quant analyst. Work in code (Python or a spreadsheet).
Inputs: <sep> [your table from question 1] </sep>, <feb> the attached IEF comparison, February 2026 </feb>, <gdp> [paste gdp_note.md] </gdp>.
Tasks:
1) For each quarter, compute OPEC minus IEA in February, in September, and the change.
2) Each agency and edition: change in demand, 2Q26 to 4Q26.
3) Plot demand by quarter: September solid, February dashed, one colour per agency.
4) Compare the 2026 GDP growth each agency assumes.
5) Print the results and two sanity checks.
Rules: only the inputs; if missing, "Not stated".
```

---

## Activity 4 · Card 4 (question 4)

Your agency's 2Q26 table: OPEC and IEA in `excerpts_OPEC_IEA.md`; EIA in `reports/2026-09_EIA_STEO.pdf`, Table 3a, p. 33 (column 2026 Q2).

```
Step 1 (step back): before using any numbers, state the identity that links world oil demand, supply and stock changes over a quarter. Which term is observed best, and which least?
Step 2 (worked example): OPEC, 2Q26 (MOMR, Table 11-1). Supply 97.3. Balance (supply minus demand) -5.6, so stocks fell by 5.6. Demand = 97.3 + 5.6 = 102.9. Check: OPEC publishes 102.9. OK.
Step 3 (your turn): apply exactly the same steps to <data>. One row: agency | edition | supply | stock draw | demand | matches the published demand?
Rules: use only <data>. State whether a positive number means a draw or a build. If a number is missing, write "VERIFY -- not in source".
<data> [paste your agency's 2Q26 table here] </data>
```

---

## Activity 5 · Card 5a (what would have to be true)

```
Role: skeptical reviewer for the CEO.
Task: what would have to be true for each agency's 2Q26 demand in <table>? Use the observed stock change in <evidence>: demand = own supply + observed draw.
Output: agency | demand with observed draw | published demand | difference (mb/d; million barrels over 91 days).
Then argue against the recommendation in <draft>, using only these numbers.
<table> [your answer 4] </table>
<evidence> [IEA observed stocks, from excerpts_OPEC_IEA.md] </evidence>
<draft> [paste ai_draft.md] </draft>
```

## Activity 5 · Card 5b (consistency check)

```
Task: check consistency between <draft> and <table>.
List every number and claim in the draft; mark each as matches | wrong | growth-vs-level confusion | not in table.
Then propose corrected wording with minimal edits (max 80 words).
<draft> [paste ai_draft.md] </draft>
<table> [your answer sheet] </table>
```

## Activity 5 · Card 5c (chain of verification)

```
Chat 1: List every checkable claim in <draft> as a question (max 6). Do not answer them.
Chat 2 (new): Answer each question using ONLY <pack>. Quote the sentence, or write "Not in pack".
Then: mark each claim in the draft as confirmed | wrong | unsupported.
<pack> [your answer sheet and the files in this data pack] </pack>
```

---

## Bonus · Meta-prompt: let the AI write the download prompt (lecturer demo)

```
I am preparing a CEO briefing on why OPEC, the IEA and the EIA disagree about 2026 oil demand. <plan> lists our questions, the data and the sources.
Write a prompt for an AI agent with web access that puts all inputs in one folder. The agent must:
- download each report and data file from the agency's own website (September and February 2026 editions);
- name files clearly, e.g. 2026-09_OPEC_MOMR.pdf;
- write a manifest: file | agency | edition | URL | question | status;
- write "NOT FOUND" and why, never another edition or an unofficial copy.
Ask me up to 3 questions first.
<plan> [paste the room's plan] </plan>
```
