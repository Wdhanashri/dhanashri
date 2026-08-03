# Week 9 — 2-D Dynamic Programming · D57–D63

**9 problems + 2 🔵 · 4 concepts · algorithm 14 (part 2 of 2)**

> ⛔ Don't start until Week 8's gate is passed — **including Part C, the transfer test.** If you passed everything except Part C, redo that first. It's the part that matters.

---

## The whole week in one line

**Two changing inputs instead of one. That's it.**

```
1-D DP        dp[i]        one thing varies      (position in an array)
2-D DP        dp[i][j]     two things vary       (position in TWO strings,
                                                  or row and column,
                                                  or index and remaining budget)
```

The four steps from Week 8 are unchanged:

```
1. write the brute-force recursion
2. notice the repeats
3. add @cache          ← now it's 2-D DP, and the cache key is a PAIR
4. convert to a table  ← optional, mechanical
```

**The only new skill is spotting the second dimension.** Ask: *"what two things change as I recurse?"*

## Open one file. Top to bottom. Don't scroll back.

| Day | File | What you learn | Problems |
|---|---|---|---|
| D57 | [d57.md](d57.md) | Two inputs → a grid of subproblems | 2D 1, 4 |
| D58 | [d58.md](d58.md) | String DP — match or skip | 2D 2, 9 |
| D59 | [d59.md](d59.md) | Target sum · state as (index, budget) | 2D 5, 3 |
| D60 | [d60.md](d60.md) | Two-pointer string DP | 2D 6, 8 |
| D61 | [d61.md](d61.md) | Space optimisation · DP on a grid | 2D 7 |
| D62 | [d62.md](d62.md) | Build day | 🔵 2D 10, 🔵 2D 11 |
| D63 | [d63.md](d63.md) | **Gate** — no new material | — |

## Guardrails

- **25 min max per problem.** Stuck → solution, log it, move on.
- **120 min max per day.** Hard stop.
- **The `dp[i][j]` English sentence goes in a comment on every single solution.** Same rule as Week 8, and it matters more here.
- **D62's two problems are both 🔵.** Behind? Skip them and clear 🟡s instead.

**Finding problems:** **neetcode.io/practice**. `2D 9` = *2-D Dynamic Programming*, 9th problem.
