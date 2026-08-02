# Anchors — the whole of Tier 1 in one page

**How to use:** once a week, and on the morning of any interview — read the *anchor only*, out loud, and try to reconstruct the concept before your eyes move right. Cover the right column with your hand.

Five minutes. Not more.

**The 8 Hinglish hooks.** These 8 concepts have a second anchor in Hindi, because for these the Hindi phrasing lands harder and sticks longer. Either version counts as a correct recall — use whichever one arrives first.

| Yaad rakho | → Concept |
|---|---|
| *"Sorted hai? Dono taraf se andar chalo."* | C-05 Opposite-end pointers |
| *"Paani utna hi rukega jitni chhoti deewar."* | C-07 Max-from-both-sides |
| *"Right se badhao, left se ghatao — peeche mat dekho."* | C-08 Window mechanics |
| *"Jo chhota hai, uska kaam ho gaya — pop kar do."* | C-12 Monotonic stack |
| *"Array mat dhoondo — jawab dhoondo."* | C-15 Search the answer space |
| *"Nakli head lagao — asli ka tension khatam."* | C-18 Dummy node |
| *"Do chaal, ek raasta — chakkar hai to milenge zaroor."* | C-19 Fast & slow pointers |
| *"Sawaal upar se neeche jaata hai, jawab neeche se upar aata hai."* | C-21 Info up vs info down |

---

| Anchor (say this out loud) | → Concept |
|---|---|
| "Spend memory, buy time — a dict kills a nested loop" | C-01 Hash map trade |
| "Counter turns 'how many' into one line" | C-02 Frequency counting |
| "Everything left × everything right" | C-03 Prefix/suffix products |
| "O(1) 'is it there' — and 'am I a sequence start'" | C-04 Set membership |
| "Sorted? Walk in from both ends" | C-05 Opposite-end pointers |
| "Same value as last? Slide past it" | C-06 Skipping duplicates |
| "Water height = min(tallest left, tallest right)" | C-07 Max-from-both-sides |
| "Grow right, shrink left, never look back" | C-08 Window mechanics |
| "Name what makes a window *valid* before you code" | C-09 The window invariant |
| "The map is the window's memory" | C-10 Window + freq map |
| "For when the answer depends on the last unresolved thing" | C-11 Stack as memory |
| "Pop everything smaller — you just found their answer" | C-12 Monotonic stack |
| "Push operands, pop on operator" | C-13 Stack for parsing |
| "One template. `while lo <= hi`. Never improvise it." | C-14 Binary search template |
| "Don't search the array — search the answer" | C-15 Search the answer space |
| "One half is always sorted — find which, then decide" | C-16 Rotated arrays |
| "prev, curr, nxt — save next *before* you cut" | C-17 Pointer surgery |
| "A fake head means no special case for the real one" | C-18 Dummy node |
| "Two speeds on one track — they meet inside the loop" | C-19 Fast & slow pointers |
| "Base case → recurse both sides → combine" | C-20 Tree recursion template |
| "Return value carries up. Parameter carries down." | C-21 Info up vs info down |
| "One loop per level — snapshot `len(q)` first" | C-22 BFS with deque |
| "Every node lives inside a (low, high) window" | C-23 BST invariant |
| "What you report ≠ what you return" | C-24 Global vs returned |
| "Preorder + `N` for empty = a unique string" | C-25 Serialize w/ null markers |

---

## Pattern-picker — when you don't know what to use

Read the *problem's* words, not the topic heading.

| The problem says… | Reach for |
|---|---|
| "duplicate", "count", "seen before", "pairs summing to" | Hash map / set |
| "sorted array" + "find a pair/triplet" | Two pointers |
| "contiguous subarray/substring" + "longest / shortest / at most k" | Sliding window |
| "next greater", "previous smaller", "how many days until" | Monotonic stack |
| "sorted" + "find one thing" | Binary search |
| "minimum capacity/speed such that it works" | Binary search on the answer |
| "cycle", "middle node", "nth from end" | Fast & slow pointers |
| "tree" + "every node" | DFS recursion |
| "level", "shortest path", "nearest" | BFS |
| "valid parentheses", "expression", "undo" | Stack |
