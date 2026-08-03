# Anchors — all 56 concepts on one page

**How to use:** cover the right column. Read the anchor aloud, reconstruct the concept, then check.

Five minutes weekly. Thirty minutes the morning of an interview.

---

## Tier 1 · Arrays → Trees

| Anchor (say this out loud) | → Concept |
|---|---|
| "Spend memory, buy time — a dict kills a nested loop" | C-01 Hash map trade |
| "Counter turns 'how many' into one line" | C-02 Frequency counting |
| "Everything left × everything right" | C-03 Prefix/suffix products |
| "O(1) 'is it there' — and 'am I a sequence start'" | C-04 Set membership |
| "Sorted? Walk in from both ends" · *"Dono taraf se andar chalo"* | C-05 Opposite-end pointers |
| "Same value as last? Slide past it" | C-06 Skipping duplicates |
| "Water height = min(tallest left, tallest right)" · *"Paani utna hi rukega jitni chhoti deewar"* | C-07 Max-from-both-sides |
| "Grow right, shrink left, never look back" · *"Right se badhao, left se ghatao"* | C-08 Window mechanics |
| "Name what makes a window *valid* before you code" | C-09 The window invariant |
| "The map is the window's memory" | C-10 Window + freq map |
| "For when the answer depends on the last unresolved thing" | C-11 Stack as memory |
| "Pop everything smaller — you just found their answer" · *"Jo chhota hai, uska kaam ho gaya"* | C-12 Monotonic stack |
| "Push operands, pop on operator" | C-13 Stack for parsing |
| "One template. `while lo <= hi`. Never improvise it." | C-14 Binary search template |
| "Don't search the array — search the answer" · *"Array mat dhoondo, jawab dhoondo"* | C-15 Search the answer space |
| "One half is always sorted — find which, then decide" | C-16 Rotated arrays |
| "prev, curr, nxt — save next *before* you cut" | C-17 Pointer surgery |
| "A fake head means no special case for the real one" · *"Nakli head lagao"* | C-18 Dummy node |
| "Two speeds on one track — they meet inside the loop" · *"Do chaal, ek raasta"* | C-19 Fast & slow pointers |
| "Base case → recurse both sides → combine" | C-20 Tree recursion template |
| "Return value carries up. Parameter carries down." · *"Sawaal upar se neeche, jawab neeche se upar"* | C-21 Info up vs info down |
| "One loop per level — snapshot `len(q)` first" | C-22 BFS with deque |
| "Every node lives inside a (low, high) window" · *"Har node apni hadd mein"* | C-23 BST invariant |
| "What you report ≠ what you return" | C-24 Global vs returned |
| "Preorder + `N` for empty = a unique string" | C-25 Serialize w/ null markers |

---

## Tier 2 · Heaps → Bits

| Anchor | → Concept |
|---|---|
| "A heap gives you the smallest thing instantly — and nothing else" | C-26 `heapq` mechanics |
| "To keep the k largest, hold a MIN-heap of size k" | C-27 The size-k heap |
| "Split the data in half; keep the two halves facing each other" | C-28 Two heaps |
| "Choose → explore → un-choose" | C-29 Backtracking template |
| "Pass `i` to reuse it. Pass `i+1` to move on." | C-30 Subsets vs permutations |
| "Cut the branch the moment it cannot succeed" | C-31 Pruning & duplicates |
| "A graph is a dict from node to its neighbours. That's it." | C-32 Adjacency list |
| "Every cell is a node. Its neighbours are up, down, left, right." | C-33 Grid as a graph |
| "A tree can't loop back. A graph can — so remember where you've been." | C-34 The visited set |
| "Put every source in the queue before you start" | C-35 Multi-source BFS |
| "Repeatedly take whatever has nothing left blocking it" | C-36 Topological sort |
| "Every group has one boss. Two nodes are together if they share a boss." | C-37 Union-Find |
| "One node per letter. Shared prefixes share nodes." | C-38 Trie |
| "BFS with a heap instead of a queue" | C-39 Dijkstra |
| "Connect all n nodes with n−1 edges, as cheaply as possible" | C-40 MST (Prim) |
| "These aren't algorithms. They're index tricks you either know or don't." | C-41 Matrix & math tricks |
| "Same recursion. Add a cache. That's DP." | C-42 Memoise the recursion |
| "Top-down asks. Bottom-up builds." | C-43 Top-down → bottom-up |
| "Say `dp[i]` in one English sentence, or you don't have the problem yet" | C-44 The state question |
| "Stand at the middle and push outwards" | C-45 Expand around centre |
| "`dp[i]` looks back at every `j < i`. Two loops, not one." | C-46 The LIS shape |
| "Take one, or take two — if the two are legal" | C-47 Unbounded choice |
| "Two things changing → `dp[i][j]`. The cache key is a pair." | C-48 Two inputs → 2-D grid |
| "Characters match → advance both. Don't match → try each, take the best." | C-49 String DP |
| "The second dimension can be a running total, a budget, or a mode" | C-50 Knapsack & target sum |
| "If you only look back one row, keep one row" | C-51 Space optimisation |
| "If the running sum goes negative, it's a burden. Drop it." | C-52 Kadane |
| "Greedy works when the local best can never be regretted — say why" | C-53 The greedy proof |
| "Sort by START to merge. Sort by END to keep the most." | C-54 Interval sorting |
| "`a ^ a = 0`. XOR everything and the pairs disappear." | C-55 XOR tricks |
| "`n & (n-1)` clears the lowest set bit" | C-56 Bitmask as a set |

---

## The pattern-picker — when you don't know what to use

Read the *problem's* words, not the topic heading.

| The problem says… | Reach for |
|---|---|
| "duplicate", "count", "seen before", "pairs summing to" | Hash map / set |
| "sorted array" + "find a pair/triplet" | Two pointers |
| "contiguous subarray/substring" + "longest / at most k" | Sliding window |
| "next greater", "previous smaller", "days until" | Monotonic stack |
| "sorted" + "find one thing" | Binary search |
| "minimum X such that it works" | Binary search on the answer |
| "cycle", "middle node", "nth from end" | Fast & slow pointers |
| "tree" + "every node" | DFS recursion |
| "level", "shortest path in an unweighted graph" | BFS |
| "top k", "kth largest", "which is best right now" (changing) | Heap |
| "all combinations / permutations / subsets" | Backtracking |
| "islands", "regions", "connected cells" | Grid DFS/BFS |
| "spreads simultaneously from several places" | Multi-source BFS |
| "prerequisites", "ordering with dependencies" | Topological sort |
| "are these connected", edges arriving over time | Union-Find |
| "prefix", "autocomplete", "starts with" | Trie |
| "shortest path" + **weights** | Dijkstra |
| "connect everything cheapest" | MST |
| "how many ways", "min/max over choices", overlapping subproblems | DP |
| two strings compared position by position | 2-D string DP |
| "maximum subarray sum" | Kadane |
| "merge / overlap / meeting rooms" | Sort intervals |
| "appears twice except one", "without extra memory" | XOR |

---

## If you have 5 minutes before an interview

Read the **anchors for your weakest tier**, out loud. Then the pattern-picker table.
