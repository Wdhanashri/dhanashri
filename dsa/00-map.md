# Tier 1 Map — 4 weeks, 60 problems, 8 of your 15 algorithms

```
                     ┌─────────────────┐
                     │  HASH / COUNT   │  W1  trade memory for time
                     └────────┬────────┘
                              │
              ┌───────────────┴───────────────┐
              │                               │
     ┌────────▼────────┐             ┌────────▼────────┐
     │  TWO POINTERS   │  W1         │     STACK       │  W2
     │  walk inward    │             │ last unresolved │
     └────────┬────────┘             └────────┬────────┘
              │                               │
     ┌────────▼────────┐             ┌────────▼────────┐
     │ SLIDING WINDOW  │  W2         │ MONOTONIC STACK │  W2
     │ grow R, shrink L│             │  next greater   │
     └─────────────────┘             └─────────────────┘

     ┌─────────────────┐             ┌─────────────────┐
     │ BINARY SEARCH   │  W3         │  LINKED LIST    │  W3
     │  halve the space│             │ pointer surgery │
     └─────────────────┘             └────────┬────────┘
                                              │ fast & slow
                                     ┌────────▼────────┐
                                     │     TREES       │  W4
                                     │  DFS  +  BFS    │
                                     └─────────────────┘
```

---

## The 15 algorithms (your real target for all 10 weeks)

Tier 1 hands you the first 8. Tier 2 hands you the rest.

| # | Algorithm | Where | |
|---|---|---|---|
| 1 | Hashing & frequency counting | W1 | ← Tier 1 |
| 2 | Two pointers | W1 | ← Tier 1 |
| 3 | Sliding window | W2 | ← Tier 1 |
| 4 | Monotonic stack | W2 | ← Tier 1 |
| 5 | Binary search (+ on the answer) | W3 | ← Tier 1 |
| 6 | Fast & slow pointers (Floyd) | W3 | ← Tier 1 |
| 7 | DFS / recursion | W4 | ← Tier 1 |
| 8 | BFS / level order | W4 | ← Tier 1 |
| 9 | Backtracking | W6 | Tier 2 |
| 10 | Heap / top-K | W6 | Tier 2 |
| 11 | Union-Find | W7 | Tier 2 |
| 12 | Topological sort | W7 | Tier 2 |
| 13 | Dijkstra | W7 | Tier 2 |
| 14 | DP: memo → tabulation | W8-9 | Tier 2 |
| 15 | Greedy + interval sorting | W10 | Tier 2 |

**By the end of Week 4, half your algorithm fluency is done.** Say that number out loud when Week 3 feels heavy.

---

## The 4 weeks

| Week | Days | NC150 sections | Problems | Gate |
|---|---|---|---|---|
| **1** | D1–D7 | Arrays & Hashing + Two Pointers | 14 | Weekly |
| **2** | D8–D14 | Sliding Window + Stack | 13 | Weekly |
| **3** | D15–D21 | Binary Search + Linked List | 15 core + 3 🔵 | Weekly |
| **4** | D22–D28 | Trees | 15 | **Tier 1 exit gate** |

Week 1 is compressed on arrays deliberately — you've covered that ground several times. We're not re-teaching it; we're testing whether it's actually *there*, then moving.

Day 7 of every week = consolidation + gate. **No new material on Day 7, ever.**

---

## The 25 concepts

| Week | Concepts |
|---|---|
| 1 | C-01 Hash map trade · C-02 Frequency counting · C-03 Prefix/suffix products · C-04 Set membership · C-05 Opposite-end pointers · C-06 Skipping duplicates · C-07 Max-from-both-sides |
| 2 | C-08 Window mechanics · C-09 The window invariant · C-10 Window + freq map · C-11 Stack as memory · C-12 Monotonic stack · C-13 Stack for parsing |
| 3 | C-14 Binary search template · C-15 Search the answer space · C-16 Rotated arrays · C-17 Pointer surgery · C-18 Dummy node · C-19 Fast & slow pointers |
| 4 | C-20 Tree recursion template · C-21 Info up vs info down · C-22 BFS with deque · C-23 BST invariant · C-24 Global vs returned answer · C-25 Serialize with null markers |

Every one of these has an anchor in `anchors.md` and a scheduled review in `ledger.md`. None of them is allowed to quietly fade.

---

## Exit criteria for Tier 1

You may start Tier 2 only when **all** of these are true:

- [ ] All 60 problems attempted, none skipped without being logged
- [ ] `ledger.md` shows **zero 🔴** and **at most three 🟡**
- [ ] Every mistake in `mistakes.md` has been re-tested at least once
- [ ] `gates/tier-1-exit.md` passed — all three parts

If you fail the exit gate, you do **not** repeat Tier 1. You repeat only the concepts that failed. Everything you passed stays passed.
