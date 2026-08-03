# The Map — 10 weeks, 150 problems, 15 algorithms

```
TIER 1 · W1-W4 · 60 problems          TIER 2 · W5-W10 · 90 problems
─────────────────────────────         ──────────────────────────────
  HASH / COUNT        W1                HEAP · BACKTRACKING     W5
  TWO POINTERS        W1                GRAPHS · TRIE · DSU     W6
  SLIDING WINDOW      W2                DIJKSTRA · MST · MATH   W7
  STACK · MONOTONIC   W2                1-D DP                  W8
  BINARY SEARCH       W3                2-D DP                  W9
  LINKED LIST         W3                GREEDY · INTERVALS ·    W10
  TREES (DFS + BFS)   W4                BIT MANIPULATION
```

---

## The 15 algorithms

| # | Algorithm | Week | |
|---|---|---|---|
| 1 | Hashing & frequency counting | W1 | Tier 1 |
| 2 | Two pointers | W1 | Tier 1 |
| 3 | Sliding window | W2 | Tier 1 |
| 4 | Monotonic stack | W2 | Tier 1 |
| 5 | Binary search (+ on the answer) | W3 | Tier 1 |
| 6 | Fast & slow pointers (Floyd) | W3 | Tier 1 |
| 7 | DFS / recursion | W4 | Tier 1 |
| 8 | BFS / level order | W4 | Tier 1 |
| 9 | Heap / top-K | W5 | **Tier 2** |
| 10 | Backtracking | W5 | **Tier 2** |
| 11 | Graph traversal · topological sort | W6 | **Tier 2** |
| 12 | Union-Find · Trie | W6 | **Tier 2** |
| 13 | Dijkstra · MST | W7 | **Tier 2** |
| 14 | DP: memo → tabulation | W8–W9 | **Tier 2** |
| 15 | Greedy + interval sorting | W10 | **Tier 2** |

---

## The 10 weeks

| Week | Days | NC150 sections | Problems | Gate |
|---|---|---|---|---|
| **1** | D1–D7 | Arrays & Hashing + Two Pointers | 14 | Weekly |
| **2** | D8–D14 | Sliding Window + Stack | 13 | Weekly |
| **3** | D15–D21 | Binary Search + Linked List | 15 + 3 🔵 | Weekly |
| **4** | D22–D28 | Trees | 15 | **Tier 1 exit** |
| **5** | D29–D35 | Heap + Backtracking | 15 + 1 🔵 | Weekly |
| **6** | D36–D42 | Graphs + Tries | 14 + 2 🔵 | Weekly |
| **7** | D43–D49 | Advanced Graphs + Math & Geometry | 11 + 3 🔵 | Weekly |
| **8** | D50–D56 | 1-D DP | 12 | Weekly |
| **9** | D57–D63 | 2-D DP | 9 + 2 🔵 | Weekly |
| **10** | D64–D70 | Greedy + Intervals + Bit | 20 + 1 🔵 | **FINAL** |

Day 7 of every week = consolidation + gate. **No new material on Day 7, ever.**

---

## The 56 concepts

| Week | Concepts |
|---|---|
| 1 | C-01 Hash map trade · C-02 Frequency counting · C-03 Prefix/suffix · C-04 Set membership · C-05 Opposite-end pointers · C-06 Skipping duplicates · C-07 Max-from-both-sides |
| 2 | C-08 Window mechanics · C-09 The window invariant · C-10 Window + freq map · C-11 Stack as memory · C-12 Monotonic stack · C-13 Stack for parsing |
| 3 | C-14 Binary search template · C-15 Search the answer space · C-16 Rotated arrays · C-17 Pointer surgery · C-18 Dummy node · C-19 Fast & slow pointers |
| 4 | C-20 Tree recursion · C-21 Info up vs down · C-22 BFS with deque · C-23 BST invariant · C-24 Global vs returned · C-25 Serialize w/ nulls |
| **5** | C-26 `heapq` mechanics · C-27 The size-k heap · C-28 Two heaps · C-29 Backtracking template · C-30 Subsets vs permutations · C-31 Pruning & duplicates |
| **6** | C-32 Adjacency list · C-33 Grid as a graph · C-34 The visited set · C-35 Multi-source BFS · C-36 Topological sort · C-37 Union-Find · C-38 Trie |
| **7** | C-39 Dijkstra · C-40 MST (Prim) · C-41 Matrix & math tricks |
| **8** | C-42 Memoise the recursion · C-43 Top-down → bottom-up · C-44 The state question · C-45 Expand around centre · C-46 The LIS shape · C-47 Unbounded choice |
| **9** | C-48 Two inputs → 2-D grid · C-49 String DP · C-50 Knapsack & target sum · C-51 Space optimisation |
| **10** | C-52 Kadane · C-53 The greedy proof · C-54 Interval sorting · C-55 XOR tricks · C-56 Bitmask as a set |

Every one has an anchor in `anchors.md` and a scheduled recall in `ledger.md`. **Tier 1 concepts keep appearing right through Week 9** — that's deliberate, and it's the only reason you'll still know them in October.

---

## Exit criteria

**Tier 1 → Tier 2:** all 60 problems attempted · zero 🔴 · `week-4/d28.md` passed.

**Tier 2 → interview-ready:**
- [ ] All 150 problems attempted, none skipped without being logged
- [ ] `ledger.md` shows **zero 🔴** and at most five 🟡
- [ ] `week-10/d70.md` passed — all four parts
- [ ] You can name the pattern for an unlabelled problem in under 30 seconds

If you fail the final gate, you do **not** repeat Tier 2. You repeat only the concepts that failed.
