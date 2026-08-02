# Week 2 — Sliding Window + Stack · D8–D14

**13 problems · 6 concepts · algorithms 3 & 4 of your 15**

> ⛔ **Do not start until Week 1's gate is passed and `ledger.md` has zero overdue rows.**

**Guardrails:** 20 min max per problem · 120 min max per day · blank page before notes · every miss → `mistakes.md`.

**Daily shape:** Cold open 10m → Learn 25m → **Blank page 5m** → Problems 60m → Teach-back 5m → Ledger 2m.

**Finding problems:** **neetcode.io/practice**. `SW 3` = *Sliding Window* section, 3rd problem. `ST 6` = *Stack*, 6th.

---

## Concepts

### C-08 · Window mechanics
**Anchor:** *"Grow right, shrink left, never look back."*
**Yaad rakho:** *"Right se badhao, left se ghatao — peeche mat dekho."*

```
s = a b c a b c b b
    L
    R→ → →           grow R while the window stays valid
      L→             when invalid, shrink from L until valid again
    Neither pointer ever moves backwards → each index touched ≤ 2× → O(n)
```

One `for r in range(n)` loop, with a `while` inside that moves `l`. Not two nested for-loops.

**The Gotcha:** the inner `while` is what makes it O(n), not O(n²) — because `l` only ever advances. Say that out loud; interviewers ask.

**Recall prompt:** *Sliding window looks like a nested loop. Why is it O(n)?*

---

### C-09 · The window invariant
**Anchor:** *"Name what makes a window valid before you code."*

| Problem | The window is valid while… |
|---|---|
| Longest Substring w/o Repeat | no character appears twice |
| Longest Repeating Char Replacement | `window_len - max_freq <= k` |
| Permutation in String | window counts == pattern counts |
| Minimum Window Substring | window covers every needed char |

Write that sentence down *first*, in English. Then the code writes itself: grow while valid, shrink while not.

**The Gotcha:** in Longest Repeating Char Replacement, `max_freq` doesn't need to be recomputed when the window shrinks. Leaving it stale is *correct* here — the answer can only be beaten by a genuinely larger `max_freq`. This looks like a bug and isn't.

**Recall prompt:** *Before coding any sliding window, what single sentence do you write?*

---

### C-10 · Window + frequency map
**Anchor:** *"The map is the window's memory."*

```python
need = Counter(t)
have = Counter()
matched = 0                       # how many chars hit their required count
# on expand: have[c] += 1; if have[c] == need[c]: matched += 1
# on shrink: if have[c] == need[c]: matched -= 1; have[c] -= 1
```

Track a `matched` counter, not `have == need`. Comparing whole dicts every step is O(26) per move and hides the real logic.

**The Gotcha:** on shrink, decrement `matched` **before** decrementing `have` — otherwise the equality check has already been broken by your own edit.

**Recall prompt:** *Min window substring — why track a `matched` counter instead of comparing two dicts?*

---

### C-11 · Stack as memory
**Anchor:** *"For when the answer depends on the last unresolved thing."*

```
"( [ { } ] )"
push (  →  [ (              a closer must match the TOP
push [  →  [ (, [           nothing else can be pending
push {  →  [ (, [, {
see  }  →  pop { ✓
```

If a problem says "matching", "nesting", "most recent", or "undo" — it's a stack.

**The Gotcha:** Min Stack (ST 2) — store `(value, min_so_far)` as pairs, so `getMin()` is O(1). Recomputing the min on demand is the trap.

**Recall prompt:** *Which four words in a problem statement mean "use a stack"?*

---

### C-12 · Monotonic stack
**Anchor:** *"Pop everything smaller — you just found their answer."*
**Yaad rakho:** *"Jo chhota hai, uska kaam ho gaya — pop kar do."*

```
temps: 73  74  75  71  69  72  76
       ↑    └─ 74 > 73, so 73's answer is "1 day" → pop it
stack holds INDICES, in decreasing temperature order
when a bigger value arrives, everything it beats gets resolved and popped
```

Each index is pushed once and popped once → O(n) despite the nested-looking `while`.

**The Gotcha:** store **indices**, not values. You almost always need the distance `i - stack[-1]`, and you can always get the value back with `arr[idx]`.

**Recall prompt:** *Monotonic stack — what do you store in it, and why not the values?*

---

### C-13 · Stack for parsing
**Anchor:** *"Push operands, pop on operator."*

```
["2","1","+","3","*"]
push 2, push 1
 "+" → pop 1, pop 2 → push 3
push 3
 "*" → pop 3, pop 3 → push 9      answer: 9
```

**The Gotcha:** order matters for `-` and `/`. The **second** value popped is the left operand: `a = stack.pop()` then `b = stack.pop()`, compute `b - a`. And Python's `//` floors toward negative infinity — Evaluate RPN wants truncation toward zero, so use `int(b / a)`.

**Recall prompt:** *RPN evaluation — you pop two values. Which one is the left operand?*

---

## Day plan

### D8 — Window basics
**Cold open:** ① *(W1)* C-05 anchor? ② 3Sum duplicate-skip spots? ③ Bucket-sort top-k?
**Learn:** C-08.
**Exercise (10 min, paper):** trace L and R on `"abcabcbb"` for Longest Substring w/o Repeat. Write the window contents and the best-so-far at every step. Do this *before* coding.

| NeetCode | Problem | Guidance | Cap |
|---|---|---|---|
| SW 1 | Best Time to Buy & Sell | Not really a window — just track `min_price` so far. Do it in 5 min as a warm-up. | 10m |
| SW 2 | Longest Substring w/o Repeat | The canonical window. Set or last-seen dict. If using a dict, `l = max(l, seen[c]+1)` — the `max` matters. | 25m |

### D9 — The invariant
**Cold open:** ① C-08 anchor? ② Why is a sliding window O(n)? ③ *(W1)* Prefix/suffix products?
**Learn:** C-09.

| NeetCode | Problem | Guidance | Cap |
|---|---|---|---|
| SW 3 | Longest Repeating Char Replacement | Invariant: `window_len - max_freq <= k`. The stale-`max_freq` subtlety is the whole lesson. | 25m |
| SW 4 | Permutation in String | Fixed-size window. Slide it and compare counts — no shrinking loop needed. | 20m |

### D10 — Window + map
**Cold open:** ① C-09 anchor? ② The invariant for Longest Repeating Char Replacement? ③ *(D8)* Why O(n)?
**Learn:** C-10.

| NeetCode | Problem | Guidance | Cap |
|---|---|---|---|
| SW 5 | Minimum Window Substring | The hardest window problem there is. Use the `matched` counter. Take the full 40 min — this one is worth it. | 40m |

### D11 — Stacks
**Cold open:** ① C-10 anchor? ② Why `matched` and not dict comparison? ③ *(D9)* C-09 anchor?
**Learn:** C-11.

| NeetCode | Problem | Guidance | Cap |
|---|---|---|---|
| ST 1 | Valid Parentheses | Map closers→openers. Check the stack is empty at the end — that's the commonly-missed case. | 10m |
| ST 2 | Min Stack | Store `(val, min_so_far)` pairs. O(1) `getMin`. | 15m |
| ST 4 | Generate Parentheses | ⚠️ This is **backtracking**, not a stack — NeetCode files it here anyway. Rule: add `(` if `open < n`, add `)` if `close < open`. A preview of Week 6. | 25m |

### D12 — Monotonic
**Cold open:** ① C-11 anchor? ② Four words that mean "stack"? ③ *(D10)* The `matched` trick?
**Learn:** C-12.

| NeetCode | Problem | Guidance | Cap |
|---|---|---|---|
| ST 5 | Daily Temperatures | The textbook monotonic stack. Store indices. | 20m |
| ST 6 | Car Fleet | Sort by position descending, then compute arrival times. A fleet forms when a car's time ≤ the stack top. | 25m |
| SW 6 | Sliding Window Maximum | Monotonic **deque** — same idea, both ends. Pop from the back while smaller; pop from the front when out of window. Filed under Sliding Window, but it's today's concept. | 30m |

### D13 — Parsing + the hard one
**Cold open:** ① C-12 anchor? ② What do you store in a monotonic stack? ③ *(D11)* Min Stack in O(1)?
**Learn:** C-13.

| NeetCode | Problem | Guidance | Cap |
|---|---|---|---|
| ST 3 | Evaluate RPN | Watch the operand order and the `int(b/a)` truncation. | 15m |
| ST 7 | Largest Rectangle in Histogram | The hardest problem in Tier 1. Monotonic increasing stack of `(index, height)`. When you pop, that bar's rectangle extends back to the popped index. **If you're stuck at 30 min, read the solution and log it — this one legitimately takes two attempts.** | 40m |

### D14 — Consolidation + Gate. **No new material.**

---

## D14 · Week 2 Gate

**Part A — Blank page (15 min).** All 6 anchors from memory, plus the window trace diagram. Then, from W1: any 4 of those 7 anchors. Pass = 5/6 this week, 3/4 from last week.

**Part B — Cold problems (45 min).** From an empty file: **Longest Substring w/o Repeat**, **Daily Temperatures**, **Minimum Window Substring**. Pass = 2/3 working.

**Part C — Out loud (10 min).** Explain **why a sliding window is O(n) and not O(n²)** in 90 seconds. This is a real interview question, asked exactly like this.

**Part D — Mistake replay (20 min).** Every `mistakes.md` row from D8–D13, cold.

**Part E — Interleaved set (20 min).** Read these five and **name the pattern only — don't solve**: *Longest Repeating Char Replacement · Longest Consecutive Sequence · Car Fleet · 3Sum · Top K Frequent*. Deliberately unlabelled — NeetCode's section headings hand you the pattern for free, and an interviewer never will.

Then update `ledger.md`. Honestly.
