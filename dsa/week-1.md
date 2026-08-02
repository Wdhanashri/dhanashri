# Week 1 — Arrays & Hashing + Two Pointers · D1–D7

**14 problems · 7 concepts · algorithms 1 & 2 of your 15**

> You've been over arrays several times. So this week is **not** a re-teach — it's a test of whether it's actually there, moving fast. If Day 1 feels easy, good: that's the point, and it will not stay easy past Day 3.

**Guardrails:** 20 min max per problem · 120 min max per day · blank page before notes · every miss → `mistakes.md`.

**Daily shape:** Cold open 10m → Learn 25m → Blank page 5m → Problems 60m → Teach-back 5m → Ledger 2m. Details in `START-HERE.md`.

---

## Concepts

### C-01 · Hash map trade
**Anchor:** *"Spend memory, buy time — a dict kills a nested loop."*

```
nested loop:  for i: for j:  →  O(n²)
with a dict:  for i: "have I seen what I need?"  →  O(n)
                      └─ the dict remembers the past for you
```

Any time you're about to write two nested loops over the same array, stop and ask: **what would I need to have remembered to do this in one pass?** Store that in a dict as you go.

**The Gotcha:** in Two Sum, store the number as the *key* and the index as the *value* — not the reverse. You look things up by value, never by index.

**Recall prompt:** *You're about to write a nested loop over one array. What question do you ask yourself instead?*

---

### C-02 · Frequency counting
**Anchor:** *"Counter turns 'how many' into one line."*

```python
from collections import Counter
Counter("aab")            # {'a': 2, 'b': 1}
Counter(a) == Counter(b)  # anagram check, one line
```

For "top k", **don't reach for a heap first.** Frequencies are bounded by `n`, so you can bucket them: `buckets[freq].append(num)`, then walk buckets from the end. That's O(n) vs the heap's O(n log k).

**The Gotcha:** `Counter` returns `0` for missing keys instead of raising `KeyError` — convenient, but it means a typo'd key fails silently.

**Recall prompt:** *Top-k frequent elements in O(n) — no heap. How?*

---

### C-03 · Prefix / suffix products
**Anchor:** *"Everything left × everything right."*

```
nums:    [1,  2,  3,  4]
prefix:  [1,  1,  2,  6]   ← product of everything BEFORE i
suffix:  [24, 12, 4,  1]   ← product of everything AFTER i
answer:  [24, 12, 8,  6]   ← prefix[i] * suffix[i]
```

Two passes, no division. The same shape solves any "for each i, combine everything on both sides" problem.

**The Gotcha:** division is banned in LC 238 for a reason — a single zero destroys it. The two-pass version handles zeros for free.

**Recall prompt:** *Product of array except self, without division — describe the two passes.*

---

### C-04 · Set membership
**Anchor:** *"O(1) 'is it there' — and 'am I a sequence start'."*

```
nums = {100, 4, 200, 1, 3, 2}
is 3 a start?  2 in set → NO, skip it
is 1 a start?  0 in set → YES, count up: 1,2,3,4 → length 4
```

The trick in Longest Consecutive Sequence: only start counting from a number whose predecessor is missing. That's what makes it O(n) instead of O(n²) — each element is walked exactly once.

**The Gotcha:** without the "is it a start" check, you re-walk every sequence from every member. It still passes small tests, then TLEs.

**Recall prompt:** *Longest consecutive sequence in O(n) — what single check keeps it linear?*

---

### C-05 · Opposite-end pointers
**Anchor:** *"Sorted? Walk in from both ends."*
**Yaad rakho:** *"Sorted hai? Dono taraf se andar chalo."*

```
[2, 7, 11, 15]   target 18
 L          R    2+15=17 too small  → L++  (only L can raise the sum)
    L       R    7+15=22 too big    → R--  (only R can lower it)
    L   R        7+11=18  ✓
```

Each move discards a whole set of possibilities, so it's O(n) instead of O(n²). It works **only** because the array is sorted — the sortedness is what makes "too small → move L" a valid deduction.

**The Gotcha:** on an unsorted array this is silently wrong, not slow. Check sortedness before reaching for it.

**Recall prompt:** *Sum is too small. Which pointer moves, and why is that the only correct choice?*

---

### C-06 · Skipping duplicates
**Anchor:** *"Same value as last? Slide past it."*

```python
if i > 0 and nums[i] == nums[i-1]:
    continue                      # outer loop: skip duplicate anchors
while l < r and nums[l] == nums[l-1]:
    l += 1                        # inner: skip after recording a hit
```

In 3Sum you must skip duplicates at **both** levels — the fixed element and the two pointers. Miss either and you emit duplicate triplets.

**The Gotcha:** the inner skip must come *after* recording the answer, not before. Skip first and you drop valid triplets.

**Recall prompt:** *3Sum — name the two places duplicates must be skipped.*

---

### C-07 · Max-from-both-sides
**Anchor:** *"Water height = min(tallest left, tallest right)."*
**Yaad rakho:** *"Paani utna hi rukega jitni chhoti deewar."*

```
     █           █
     █  ~ ~ ~ ~  █      water above a bar =
     █  █     █  █      min(maxLeft, maxRight) - height[i]
  ───┴──┴─────┴──┴───
```

Two pointers, tracking `maxL` and `maxR`. **Always move the smaller side inward** — because that side is the binding constraint, its answer is already fully determined.

**The Gotcha:** the water is bounded by the *smaller* of the two maxes. Getting this backwards is the single most common bug in LC 42.

**Recall prompt:** *Trapping rain water — which pointer do you move, and what makes that safe?*

---

## Day plan

### D1 — Hashing basics
**Cold open:** none (day one). **Learn:** C-01, C-02.
**Exercise (10 min, by hand, no IDE):** on paper, trace a dict for `nums=[3,2,4], target=6`. Write the dict's contents after each step. Then, without looking, write Two Sum from scratch in the editor.

| # | Problem | Guidance | Cap |
|---|---|---|---|
| 217 | Contains Duplicate | Set, one pass. If you wrote `if nums.count(x) > 1` — that's O(n²). Fix it. | 10m |
| 242 | Valid Anagram | `Counter(s) == Counter(t)`. Then **write the manual dict version too** — interviewers ask for it. | 10m |
| 1 | Two Sum | Dict of `value → index`. Check for the complement *before* inserting the current number. | 15m |

### D2 — Grouping & counting
**Cold open (notes closed):** ① Anchor for C-01? ② Two Sum: what's the key, what's the value? ③ Top-k in O(n) — no heap — how?
**Learn:** C-02 applied.

| # | Problem | Guidance | Cap |
|---|---|---|---|
| 49 | Group Anagrams | `defaultdict(list)`, key = `tuple(count_of_26)`. Sorted-string keys work too but are O(k log k) — know both and say which is faster. | 20m |
| 347 | Top K Frequent | **Bucket sort by frequency.** Index = count, value = list of nums. Walk from the back. Say "O(n), no heap" out loud. | 20m |

### D3 — Prefix thinking
**Cold open:** ① C-02 anchor? ② Bucket-sort top-k — what's the array indexed by? ③ Two Sum key/value again.
**Learn:** C-03.

| # | Problem | Guidance | Cap |
|---|---|---|---|
| 238 | Product Except Self | Two passes. Build the prefix into the output array, then multiply by a running suffix. O(1) extra space. | 20m |
| 36 | Valid Sudoku | Three `defaultdict(set)`: rows, cols, boxes. **Box key = `(r//3, c//3)`** — that one line is the whole problem. | 20m |

### D4 — Sets
**Cold open:** ① C-03 anchor? ② Sudoku box key formula? ③ *(D1 review)* C-01 anchor?
**Learn:** C-04.

| # | Problem | Guidance | Cap |
|---|---|---|---|
| 128 | Longest Consecutive | Set + the "is `n-1` absent?" start check. Without it you get O(n²). | 20m |
| 271 | Encode/Decode Strings | Length-prefix: `"4#word"`. **LeetCode Premium** — solve it free on neetcode.io. Don't lose 20 minutes to the paywall. | 15m |

### D5 — Two pointers
**Cold open:** ① C-04 anchor? ② What makes Longest Consecutive linear? ③ *(D3)* Prefix/suffix in one line?
**Learn:** C-05, C-06.
**Exercise (10 min, paper):** trace L/R on `[1,2,3,4,6]`, target 9. Write both pointers after each step, and *why* each moved.

| # | Problem | Guidance | Cap |
|---|---|---|---|
| 125 | Valid Palindrome | Two pointers + `.isalnum()`. Skip non-alphanumerics on both sides *before* comparing. | 10m |
| 167 | Two Sum II | Pure C-05. Should take 5 minutes. If it doesn't, C-05 isn't solid — mark it 🔴. | 10m |
| 15 | 3Sum | Sort → fix `i` → two pointers on the rest. Skip duplicates at **both** levels (C-06). The hardest problem this week. | 30m |

### D6 — Two pointers, harder
**Cold open:** ① C-05 anchor? ② 3Sum — the two duplicate-skip spots? ③ *(D4)* Consecutive-sequence start check?
**Learn:** C-07.

| # | Problem | Guidance | Cap |
|---|---|---|---|
| 11 | Container With Most Water | Always move the **shorter** wall. Be able to say why moving the taller one can never help. | 20m |
| 42 | Trapping Rain Water | Two pointers + `maxL`/`maxR`. Move the smaller side. Hard — but it's C-05 and C-07 stacked, nothing new. | 30m |

### D7 — Consolidation + Gate. **No new material.**
See below.

---

## D7 · Week 1 Gate

**Part A — Blank page (15 min, notes closed).** Write all 7 anchors from memory. Then draw the prefix/suffix diagram and the two-pointer trace. Pass = 6/7 anchors unprompted.

**Part B — Cold problems (45 min).** Re-solve, from an empty file, no notes: **1**, **238**, **15**. Pass = 2/3 fully working.

**Part C — Out loud (10 min).** Explain **3Sum** to a non-programmer in 2 minutes: why sorting first, why two pointers, why the duplicate skips. Pass = no notes, no stalling.

**Part D — Mistake replay (20 min).** Re-solve every row in `mistakes.md` from this week. Any repeat → that concept drops to 🔴.

### Then update the ledger
Mark each concept 🟢 / 🟡 / 🔴 honestly. **Honesty here is the entire system.** Marking a shaky concept 🟢 to feel good means it gets scheduled 16 days out and you meet it again the week before your interview, gone.

**Failed the gate?** Don't redo the week — that's just rereading with extra steps. Take only the failed concepts back to +1 day and re-teach from the anchor. Everything you passed stays passed.
