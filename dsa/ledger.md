# Recall Ledger — Tier 1

> **Open this before anything else, every day.** It decides your session.
> Anything with `NEXT REVIEW ≤ today` is overdue. Overdue beats new material, always.

**Status:** 🔴 fragile (relearn) · 🟡 shaky (recalled with effort) · 🟢 solid (fast, cold, out loud)
**Leaves the schedule only after 🟢 twice in a row.** One good day is noise.

**After each review, update the date:**
- 🟢 → next interval doubles (+1 → +3 → +7 → +16 → +35)
- 🟡 → repeat the same interval
- 🔴 → back to **+1 day**, and re-teach from the anchor up

**Day numbers:** W1 = D1–D7 · W2 = D8–D14 · W3 = D15–D21 · W4 = D22–D28. `D29+` = during Tier 2 (that's intentional — Tier 1 must stay alive while you learn Tier 2).

---

## Week 1 — Arrays, Hashing, Two Pointers

| # | Concept | Anchor | Taught | Scheduled reviews | Done | Status | NEXT |
|---|---|---|---|---|---|---|---|
| C-01 | Hash map trade | "Spend memory, buy time — a dict kills a nested loop" | D1 | D2, D4, D8, D17 | | 🔴 | **D2** |
| C-02 | Frequency counting | "Counter turns 'how many' into one line" | D1 | D2, D4, D8, D17 | | 🔴 | **D2** |
| C-03 | Prefix/suffix products | "Everything left × everything right" | D3 | D4, D6, D10, D19 | | 🔴 | **D4** |
| C-04 | Set membership | "O(1) 'is it there' — and 'am I a sequence start'" | D4 | D5, D7, D11, D20 | | 🔴 | **D5** |
| C-05 | Opposite-end pointers | "Sorted? Walk in from both ends" | D5 | D6, D8, D12, D21 | | 🔴 | **D6** |
| C-06 | Skipping duplicates | "Same value as last? Slide past it" | D5 | D6, D8, D12, D21 | | 🔴 | **D6** |
| C-07 | Max-from-both-sides | "Water height = min(tallest left, tallest right)" | D6 | D7, D9, D13, D22 | | 🔴 | **D7** |

## Week 2 — Sliding Window, Stack

| # | Concept | Anchor | Taught | Scheduled reviews | Done | Status | NEXT |
|---|---|---|---|---|---|---|---|
| C-08 | Window mechanics | "Grow right, shrink left, never look back" | D8 | D9, D11, D15, D24 | | 🔴 | **D9** |
| C-09 | The window invariant | "Name what makes a window *valid* before you code" | D9 | D10, D12, D16, D25 | | 🔴 | **D10** |
| C-10 | Window + freq map | "The map is the window's memory" | D10 | D11, D13, D17, D26 | | 🔴 | **D11** |
| C-11 | Stack as memory | "For when the answer depends on the last unresolved thing" | D11 | D12, D14, D18, D27 | | 🔴 | **D12** |
| C-12 | Monotonic stack | "Pop everything smaller — you just found their answer" | D12 | D13, D15, D19, D28 | | 🔴 | **D13** |
| C-13 | Stack for parsing | "Push operands, pop on operator" | D13 | D14, D16, D20, D29 | | 🔴 | **D14** |

## Week 3 — Binary Search, Linked List

| # | Concept | Anchor | Taught | Scheduled reviews | Done | Status | NEXT |
|---|---|---|---|---|---|---|---|
| C-14 | Binary search template | "One template. `while lo <= hi`. Never improvise it." | D15 | D16, D18, D22, D31 | | 🔴 | **D16** |
| C-15 | Search the answer space | "Don't search the array — search the answer" | D16 | D17, D19, D23, D32 | | 🔴 | **D17** |
| C-16 | Rotated arrays | "One half is always sorted — find which, then decide" | D17 | D18, D20, D24, D33 | | 🔴 | **D18** |
| C-17 | Pointer surgery | "prev, curr, nxt — save next *before* you cut" | D18 | D19, D21, D25, D34 | | 🔴 | **D19** |
| C-18 | Dummy node | "A fake head means no special case for the real one" | D18 | D19, D21, D25, D34 | | 🔴 | **D19** |
| C-19 | Fast & slow pointers | "Two speeds on one track — they meet inside the loop" | D19 | D20, D22, D26, D35 | | 🔴 | **D20** |

## Week 4 — Trees

| # | Concept | Anchor | Taught | Scheduled reviews | Done | Status | NEXT |
|---|---|---|---|---|---|---|---|
| C-20 | Tree recursion template | "Base case → recurse both sides → combine" | D22 | D23, D25, D29, D38 | | 🔴 | **D23** |
| C-21 | Info up vs info down | "Return value carries up. Parameter carries down." | D23 | D24, D26, D30, D39 | | 🔴 | **D24** |
| C-22 | BFS with deque | "One loop per level — snapshot `len(q)` first" | D24 | D25, D27, D31, D40 | | 🔴 | **D25** |
| C-23 | BST invariant | "Every node lives inside a (low, high) window" | D25 | D26, D28, D32, D41 | | 🔴 | **D26** |
| C-24 | Global vs returned | "What you report ≠ what you return" | D26 | D27, D29, D33, D42 | | 🔴 | **D27** |
| C-25 | Serialize w/ null markers | "Preorder + `N` for empty = a unique string" | D27 | D28, D30, D34, D43 | | 🔴 | **D28** |

---

## Problem tracker

Tick only when you can **re-derive it cold**, not when you've read the solution.

**W1** — 217 ☐ · 242 ☐ · 1 ☐ · 49 ☐ · 347 ☐ · 238 ☐ · 36 ☐ · 128 ☐ · 271 ☐ · 125 ☐ · 167 ☐ · 15 ☐ · 11 ☐ · 42 ☐

**W2** — 121 ☐ · 3 ☐ · 424 ☐ · 567 ☐ · 76 ☐ · 20 ☐ · 155 ☐ · 150 ☐ · 739 ☐ · 22 ☐ · 853 ☐ · 84 ☐ · 239 ☐

**W3** — 704 ☐ · 74 ☐ · 875 ☐ · 153 ☐ · 33 ☐ · 981 ☐ · 206 ☐ · 21 ☐ · 143 ☐ · 19 ☐ · 141 ☐ · 287 ☐ · 2 ☐ · 138 ☐ · 146 ☐ · 🔵4 ☐ · 🔵23 ☐ · 🔵25 ☐

**W4** — 226 ☐ · 104 ☐ · 543 ☐ · 110 ☐ · 100 ☐ · 572 ☐ · 102 ☐ · 199 ☐ · 235 ☐ · 98 ☐ · 230 ☐ · 1448 ☐ · 124 ☐ · 105 ☐ · 297 ☐

🔵 = stretch. Drop these first if you're behind. Never drop a review to save a stretch problem.
