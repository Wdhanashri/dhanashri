# Week 3 — Binary Search + Linked List · D15–D21

**15 problems + 3 stretch · 6 concepts · algorithms 5 & 6 of your 15**

> ⛔ **Do not start until Week 2's gate is passed and `ledger.md` has zero overdue rows.**

**Guardrails:** 20 min max per problem · 120 min max per day · blank page before notes · every miss → `mistakes.md`.

**Daily shape:** Cold open 10m → Learn 25m → **Blank page 5m** → Problems 60m → Teach-back 5m → Ledger 2m.

---

## Concepts

### C-14 · Binary search template
**Anchor:** *"One template. `while lo <= hi`. Never improvise it."*

```python
lo, hi = 0, len(nums) - 1
while lo <= hi:                    # <= , not <
    mid = (lo + hi) // 2
    if nums[mid] == target: return mid
    elif nums[mid] < target: lo = mid + 1
    else: hi = mid - 1
return -1
```

Memorise this shape exactly. Every binary search bug in the world is `<` vs `<=`, or forgetting the `±1`. Type it from memory every day this week until your fingers know it.

**The Gotcha:** `lo = mid` (without `+1`) is an infinite loop. If your submission times out on a binary search, that's the bug 90% of the time.

**Recall prompt:** *Write the binary search template from memory. Where do the `+1` and `-1` go?*

---

### C-15 · Search the answer space
**Anchor:** *"Don't search the array — search the answer."*
**Yaad rakho:** *"Array mat dhoondo — jawab dhoondo."*

```
Koko eating bananas. Speeds 1…max(piles):

speed:  1   2   3   4   5   6   7   8
        ✗   ✗   ✗   ✓   ✓   ✓   ✓   ✓      ← too slow │ fast enough
        ────────────┼───────────────
              find this boundary → binary search on IT
```

The trigger phrase is **"minimum X such that it works"** or **"maximum X such that it still fits."** The array isn't sorted — but the *answers* are, because feasibility is monotonic: if speed 5 works, so does 6.

**The Gotcha:** you need a `feasible(x)` helper that returns True/False. Write that function *first*, test it alone, then wrap binary search around it.

**Recall prompt:** *Which two phrasings in a problem mean "binary search on the answer"?*

---

### C-16 · Rotated arrays
**Anchor:** *"One half is always sorted — find which, then decide."*

```
[4, 5, 6, 7, 0, 1, 2]
 └── sorted ──┘  mid=7
                 nums[lo] <= nums[mid]  →  LEFT half is sorted
                 is target inside [lo…mid]?  yes → hi = mid-1
                                             no  → lo = mid+1
```

A rotated array is two sorted runs. Compare `nums[mid]` to `nums[lo]` to learn which side is clean, then ask whether the target lives in that clean range.

**The Gotcha:** decide using the *sorted* half only. Reasoning about the messy half is where everyone goes wrong.

**Recall prompt:** *Rotated sorted array — what single comparison tells you which half is sorted?*

---

### C-17 · Pointer surgery
**Anchor:** *"prev, curr, nxt — save next before you cut."*

```
prev   curr   nxt
 None → [1] → [2] → [3]
        
nxt = curr.next        ← SAVE FIRST, or you lose the rest of the list
curr.next = prev       ← cut and re-point
prev = curr            ← shuffle forward
curr = nxt
```

Those four lines, in that order, are the whole of linked-list reversal. Never write them from logic under pressure — write them from muscle memory.

**The Gotcha:** reassigning `curr.next` before saving `nxt` orphans everything downstream. Draw the list on paper before you code — every single time.

**Recall prompt:** *Reverse a linked list. Say the four lines in order.*

---

### C-18 · Dummy node
**Anchor:** *"A fake head means no special case for the real one."*
**Yaad rakho:** *"Nakli head lagao — asli ka tension khatam."*

```python
dummy = ListNode(0)
dummy.next = head
# ... do the work using dummy ...
return dummy.next        # never `return head` — head may have been removed
```

Use it whenever the *first* node might be deleted, moved, or merged. It converts "what if it's the head?" from a special case into an ordinary one.

**The Gotcha:** always `return dummy.next`. Returning `head` is the classic bug when the original head got removed.

**Recall prompt:** *When do you add a dummy node, and what do you return?*

---

### C-19 · Fast & slow pointers
**Anchor:** *"Two speeds on one track — they meet inside the loop."*
**Yaad rakho:** *"Do chaal, ek raasta — chakkar hai to milenge zaroor."*

```
slow →  one step        If there's a cycle, fast gains exactly 1 step
fast →→ two steps       per move on slow — so it MUST catch up.
                        No cycle → fast simply runs off the end.
```

Three uses: **cycle detection** (do they meet?), **middle node** (when fast ends, slow is at the middle), **cycle start** (after meeting, reset one pointer to head and walk both at speed 1 — they meet at the entrance).

**The Gotcha:** LC 287 (Find the Duplicate) is this algorithm on an *array*, where `i → nums[i]` is the "next pointer." Nothing about it looks like a linked list. That disguise is the entire test.

**Recall prompt:** *Why must fast and slow meet if a cycle exists?*

---

## Day plan

### D15 — The template
**Cold open:** ① *(W2)* C-12 anchor? ② Why is a sliding window O(n)? ③ RPN — which pop is the left operand?
**Learn:** C-14.
**Exercise (10 min):** type the template from memory, 3 times, closing the file between attempts. Yes, three.

| # | Problem | Guidance | Cap |
|---|---|---|---|
| 704 | Binary Search | The template, verbatim. 5 minutes. | 10m |
| 74 | Search a 2D Matrix | Treat it as one flat sorted array of length `m*n`. Convert: `row = mid // n`, `col = mid % n`. | 20m |

### D16 — On the answer
**Cold open:** ① C-14 anchor? ② Where do `+1`/`-1` go? ③ *(W2)* Monotonic stack — store what?
**Learn:** C-15.

| # | Problem | Guidance | Cap |
|---|---|---|---|
| 875 | Koko Eating Bananas | Write `hours_needed(speed)` **first**, alone. Then binary search 1…max(piles). | 25m |
| 153 | Find Min in Rotated Array | Compare `nums[mid]` to `nums[hi]`, not `nums[lo]`. Cleaner, fewer cases. | 20m |

### D17 — Rotation
**Cold open:** ① C-15 anchor (Hinglish counts)? ② Two phrasings that mean "search the answer"? ③ *(D15)* Template from memory.
**Learn:** C-16.

| # | Problem | Guidance | Cap |
|---|---|---|---|
| 33 | Search in Rotated Sorted Array | Find the sorted half, ask if the target is inside it. Draw the two runs before coding. | 30m |
| 981 | Time Based Key-Value Store | `defaultdict(list)` + binary search on timestamps for the largest value ≤ target. | 25m |

### D18 — Pointers
**Cold open:** ① C-16 anchor? ② Which comparison finds the sorted half? ③ *(D16)* Koko — what's the helper function?
**Learn:** C-17, C-18.
**Exercise (10 min, paper):** draw `1→2→3→None`. Redraw the arrows after *each* of the four reversal lines. Then code 206 without looking.

| # | Problem | Guidance | Cap |
|---|---|---|---|
| 206 | Reverse Linked List | Pure C-17. Do it iteratively, then recursively. Both should become automatic. | 15m |
| 21 | Merge Two Sorted Lists | Dummy node (C-18). Attach the remainder at the end — don't loop it out. | 15m |
| 143 | Reorder List | Three steps: find middle → reverse second half → interleave. Three things you already know, stacked. | 30m |

### D19 — Fast & slow
**Cold open:** ① C-17 — four lines in order? ② C-18 — what do you return? ③ *(D17)* Sorted-half comparison?
**Learn:** C-19.

| # | Problem | Guidance | Cap |
|---|---|---|---|
| 19 | Remove Nth From End | Fast goes `n` ahead, then both walk together. Dummy node handles "remove the head." | 20m |
| 141 | Linked List Cycle | Floyd's, five lines. | 10m |
| 287 | Find the Duplicate Number | Floyd's on an array. `i → nums[i]` is the pointer. Read C-19's Gotcha again before starting. | 30m |

### D20 — Building things
**Cold open:** ① C-19 anchor? ② Why must fast and slow meet? ③ *(D18)* Dummy node — when?
**Learn:** nothing new. Today is pure application — that's deliberate.

| # | Problem | Guidance | Cap |
|---|---|---|---|
| 2 | Add Two Numbers | Dummy node + a `carry`. Loop while `l1 or l2 or carry`. | 20m |
| 138 | Copy List with Random Pointer | Two passes with a `{old_node: new_node}` dict. Pass 1 clones, pass 2 wires pointers. | 25m |
| 146 | LRU Cache | Dict + doubly linked list. **A genuine interview favourite — expect it.** Use dummy head *and* dummy tail; it removes every edge case. | 40m |

### D21 — Consolidation + Gate. **No new material.**

---

## D21 · Week 3 Gate

**Part A — Blank page (15 min).** All 6 anchors + the binary search template + the 4 reversal lines, from memory. Pass = template perfect, 5/6 anchors.

**Part B — Cold problems (45 min).** From an empty file: **33**, **206**, **875**. Pass = 2/3 working, and the template typed without hesitation.

**Part C — Out loud (10 min).** Explain **Floyd's cycle detection** in 2 minutes — including *why* they must meet. This is asked verbatim in interviews.

**Part D — Mistake replay (20 min).** Every `mistakes.md` row from D15–D20, cold.

**Part E — Interleaved set (20 min).** Name the pattern only, don't solve: LC 875 · LC 3 · LC 143 · LC 42 · LC 739 · LC 128.

### 🔵 Stretch — only if the gate passed and nothing is overdue
| # | Problem | Guidance |
|---|---|---|
| 4 | Median of Two Sorted Arrays | Genuinely hard. Binary search on the *partition*, not the values. Skip without guilt if short on time. |
| 23 | Merge k Sorted Lists | Divide & conquer pairs, or a heap (Week 6 preview). |
| 25 | Reverse Nodes in k-Group | C-17 applied k at a time. Draw it, always. |

Then update `ledger.md`.
