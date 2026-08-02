# Week 4 — Trees · D22–D28

**15 problems · 6 concepts · algorithms 7 & 8 of your 15 — Tier 1 finishes here**

> ⛔ **Do not start until Week 3's gate is passed and `ledger.md` has zero overdue rows.**

**Guardrails:** 20 min max per problem · 120 min max per day · blank page before notes · every miss → `mistakes.md`.

**Daily shape:** Cold open 10m → Learn 25m → **Blank page 5m** → Problems 60m → Teach-back 5m → Ledger 2m.

---

## Concepts

### C-20 · Tree recursion template
**Anchor:** *"Base case → recurse both sides → combine."*

```python
def solve(node):
    if not node: return <identity>        # 1. base case
    L = solve(node.left)                  # 2. trust the recursion
    R = solve(node.right)
    return <combine L, R, node.val>       # 3. combine
```

Almost every tree problem is this shape with a different `<identity>` and `<combine>`. Max depth: identity `0`, combine `1 + max(L, R)`. Same tree: identity `True`, combine `and`.

**The Gotcha:** trust the recursive call. Do not trace it three levels deep in your head — that's what overloads you. Assume `solve(node.left)` returns the right answer for that subtree, and only write the combine step.

**Recall prompt:** *Write the three-line tree recursion skeleton and name what changes between problems.*

---

### C-21 · Info up vs info down
**Anchor:** *"Return value carries up. Parameter carries down."*
**Yaad rakho:** *"Sawaal upar se neeche jaata hai, jawab neeche se upar aata hai."*

```
            (5)          ← parameters travel DOWN:  bounds, depth, path-so-far
           ↙   ↘
        (3)     (8)
       ↗   ↖
      return values travel UP:  height, count, sum, found?
```

Ask one question before coding any tree problem: **does the child need to know something from above, or does the parent need something from below?** Down → add a parameter. Up → use the return value. Both → do both.

**The Gotcha:** BST validation needs info going *down* (the low/high bounds). Checking only `left.val < node.val < right.val` locally is the single most common wrong answer to LC 98.

**Recall prompt:** *A child needs to know a bound from its ancestor. Return value or parameter?*

---

### C-22 · BFS with deque
**Anchor:** *"One loop per level — snapshot `len(q)` first."*

```python
q = deque([root])
while q:
    level_size = len(q)              # ← snapshot BEFORE the inner loop
    for _ in range(level_size):
        node = q.popleft()
        ...
        if node.left:  q.append(node.left)
        if node.right: q.append(node.right)
```

That `level_size` snapshot is what separates levels. Without it, you can't tell where one level ends.

**The Gotcha:** `deque` and `popleft()`, never a list with `pop(0)` — that's O(n) each call and turns your BFS into O(n²).

**Recall prompt:** *Level-order traversal — what must you capture before the inner loop, and why?*

---

### C-23 · BST invariant
**Anchor:** *"Every node lives inside a (low, high) window."*
**Yaad rakho:** *"Har node apni hadd ke andar rehta hai."*

```
              (5)              window: (-inf, +inf)
            ↙     ↘
         (3)       (8)         left: (-inf, 5)   right: (5, +inf)
        ↙   ↘
     (1)     (4)               (-inf,3)   (3,5)
```

Two facts do all the work: (1) each node carries an inherited range, and (2) **an inorder traversal of a BST is sorted** — which instantly solves "kth smallest."

**The Gotcha:** LC 230 doesn't need a full traversal. Do an inorder walk and stop at the kth node. Sorting the whole tree wastes the BST property you were being tested on.

**Recall prompt:** *Two ways to validate a BST. Which one is correct and why is the other wrong?*

---

### C-24 · Global vs returned
**Anchor:** *"What you report ≠ what you return."*

```
Diameter at this node = L_height + R_height     ← the ANSWER (goes to a global max)
Height returned to parent = 1 + max(L, R)       ← what the PARENT needs
```

When those two differ, keep a `self.best` (or `nonlocal best`), update it at every node, and return the *other* thing. Diameter, max path sum, and longest univalue path are all this exact pattern.

**The Gotcha:** in LC 124, a negative subtree sum should contribute `0`, not its negative value — you're allowed to just not take that branch. Use `max(0, solve(child))`.

**Recall prompt:** *Diameter of a binary tree — what goes to the global, what goes to the parent?*

---

### C-25 · Serialize with null markers
**Anchor:** *"Preorder + `N` for empty = a unique string."*

```
      (1)
     ↙   ↘            →  "1,2,N,N,3,N,N"
   (2)   (3)              nulls make the structure unambiguous
```

Preorder alone is ambiguous; preorder **with explicit nulls** is not. Deserialize with an index pointer and the same preorder order.

**The Gotcha:** preorder + inorder (LC 105) also reconstructs a tree uniquely — but only when values are distinct. Know both, and know why each works.

**Recall prompt:** *Why can't you serialize a tree with preorder alone?*

---

## Day plan

### D22 — The template
**Cold open:** ① *(W3)* C-19 anchor? ② Binary search template from memory. ③ Dummy node — what do you return?
**Learn:** C-20.

| # | Problem | Guidance | Cap |
|---|---|---|---|
| 226 | Invert Binary Tree | Swap children, recurse. 5 lines. | 10m |
| 104 | Maximum Depth | The template with identity `0`. Also do the BFS version — you'll need it on D24. | 15m |
| 543 | Diameter | Your first taste of C-24. Struggle with it today; the concept lands properly on D26. | 25m |

### D23 — Up and down
**Cold open:** ① C-20 skeleton, written out? ② What changes between tree problems? ③ *(W3)* Floyd's — why do they meet?
**Learn:** C-21.

| # | Problem | Guidance | Cap |
|---|---|---|---|
| 110 | Balanced Binary Tree | Return height *and* balanced-ness together (a tuple, or `-1` as a sentinel). O(n), not O(n²). | 25m |
| 100 | Same Tree | Two-tree recursion. Base cases first: both null, one null, values differ. | 10m |
| 572 | Subtree of Another Tree | Uses `isSameTree` as a helper. Notice you're reusing yesterday's function — that's how real code works. | 20m |

### D24 — BFS
**Cold open:** ① C-21 anchor (Hinglish counts)? ② Bound from an ancestor — parameter or return? ③ *(D22)* C-20 skeleton?
**Learn:** C-22.

| # | Problem | Guidance | Cap |
|---|---|---|---|
| 102 | Level Order Traversal | The C-22 template, verbatim. | 20m |
| 199 | Right Side View | Same BFS, take the last node of each level. One-line change from 102 — notice that. | 20m |

### D25 — BSTs
**Cold open:** ① C-22 anchor? ② What do you snapshot before the inner loop? ③ *(D23)* Balanced tree in O(n) — how?
**Learn:** C-23.

| # | Problem | Guidance | Cap |
|---|---|---|---|
| 235 | LCA of a BST | Walk down: both smaller → go left, both bigger → go right, else you're standing on the answer. | 15m |
| 98 | Validate BST | Pass `(low, high)` down. Re-read C-21's Gotcha before you start. | 25m |
| 230 | Kth Smallest in BST | Inorder, stop at k. Don't build the whole list. | 20m |

### D26 — Global answers
**Cold open:** ① C-23 anchor? ② Two ways to validate a BST — which is wrong? ③ *(D24)* Why `deque` and not a list?
**Learn:** C-24.

| # | Problem | Guidance | Cap |
|---|---|---|---|
| 1448 | Count Good Nodes | Max-so-far travels **down** as a parameter (C-21). Count travels up. | 20m |
| 124 | Binary Tree Max Path Sum | The hardest tree problem. `max(0, child)` and a global best. Go back and re-do **543** right after — same skeleton, and you'll feel it click. | 40m |

### D27 — Reconstruction
**Cold open:** ① C-24 anchor? ② Diameter — global vs returned? ③ *(D25)* BST inorder property?
**Learn:** C-25.

| # | Problem | Guidance | Cap |
|---|---|---|---|
| 105 | Build Tree from Preorder+Inorder | `preorder[0]` is the root; find it in inorder to split left/right. Use a value→index dict to avoid an O(n) search each time. | 30m |
| 297 | Serialize and Deserialize | Preorder with `N` markers. Deserialize with a moving index. | 30m |

### D28 — **TIER 1 EXIT GATE.** See `gates/tier-1-exit.md`.
