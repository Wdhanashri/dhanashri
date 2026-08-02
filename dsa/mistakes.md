# Mistake Book

> Your most valuable file. These are not failures — they are the exact list of things that would have cost you an offer, found early enough to fix.
>
> **Rule: nothing you got wrong leaves this file until you've re-solved it cold, twice.**

**Tags:** `concept-gap` (didn't know it) · `pattern-misfire` (wrong tool) · `edge-case` · `careless` (knew it, slipped) · `forgot-syntax` · `time-panic`

---

| Day | Problem / Question | What I did | What was right | Tag | Re-test on | ✅ |
|---|---|---|---|---|---|---|
| | | | | | | |

---

## Re-test protocol

When a re-test date arrives:

1. **Don't read the row.** Just the problem name. Solve it cold.
2. Solved it → tick ✅. Second consecutive tick → row retires.
3. Failed it again → the *concept* drops to 🔴 in `ledger.md`, and you re-teach from the anchor. Repeated failure means the concept was never learned, not that you were unlucky.

## Monthly diagnosis

Count your tags. The dominant one tells you what to actually fix:

| Dominant tag | The real fix — **not** "study more" |
|---|---|
| `concept-gap` | Re-teach from the anchor. This is genuine and normal. |
| `pattern-misfire` | Drill the pattern-picker table in `anchors.md`. Read problems, name the pattern, don't solve. 20 problems in 15 minutes. |
| `edge-case` | Build a fixed pre-submit checklist: empty · one element · all duplicates · negatives · overflow · `None`. Run it every time. |
| `careless` | Not a knowledge problem. Slow down for 60 seconds before you submit. More hours will not help this. |
| `forgot-syntax` | Make a one-page Python snippet sheet. `heapq`, `deque`, `Counter`, custom sort. Type it from memory weekly. |
| `time-panic` | Do timed sets, not harder problems. The bottleneck is nerves, not skill. |
