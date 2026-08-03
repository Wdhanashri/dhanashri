# Week 8 — 1-D Dynamic Programming · D50–D56

**12 problems · 6 concepts · algorithm 14 of your 15 (part 1 of 2)**

> ⛔ Don't start until Week 7's gate is passed and **`ledger.md` has zero 🔴**. That bar is stricter than usual and it's deliberate — see `week-7/d49.md`.

---

## Read this before D50

DP is the block people fear. Here is the honest version:

> **DP is the recursion you already write, plus a dictionary.**

That's it. You wrote recursive tree solutions in Week 4 without blinking. DP is the same recursion applied to a problem where the same subproblem comes up twice — so you cache the answer.

The reason it *feels* hard is that people are taught the table first. **We do it in the order that actually works:**

```
1. write the brute-force recursion       ← you can already do this
2. notice it recomputes the same thing
3. add @cache                            ← now it's "top-down DP". Done.
4. only then, convert to a table         ← optional, mechanical
```

**Every problem this week follows those four steps.** If you can do step 1, you can do DP.

## Open one file. Top to bottom. Don't scroll back.

| Day | File | What you learn | Problems |
|---|---|---|---|
| D50 | [d50.md](d50.md) | Memoise the recursion | 1D 1, 2 |
| D51 | [d51.md](d51.md) | Top-down → bottom-up | 1D 3, 4 |
| D52 | [d52.md](d52.md) | The state question | 1D 8, 10 |
| D53 | [d53.md](d53.md) | Expand around centre | 1D 5, 6 |
| D54 | [d54.md](d54.md) | The LIS shape | 1D 11, 12 |
| D55 | [d55.md](d55.md) | Unbounded choice · running product | 1D 7, 9 |
| D56 | [d56.md](d56.md) | **Gate** — no new material | — |

## Guardrails

- **25 min max per problem this week** (up from 20 — DP genuinely takes longer).
- **120 min max per day.** Hard stop.
- **Write the recursion before the table. Always.** A table you can't derive is a table you'll forget.
- **Every miss → `mistakes.md`.**

**Finding problems:** **neetcode.io/practice**. `1D 8` = *1-D Dynamic Programming*, 8th problem.
