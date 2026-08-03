# Reasoning — S4, S5

**One session per sitting. ~75 min. Stop at the horizontal rule.**

> Reasoning has almost no formulas. It's **pattern recognition under a clock** — which means the win comes from knowing the handful of shapes a question can take, so you spend your seconds solving instead of wondering.

---
---

# S4 · Series, codes, relations, directions

## ⓪ Cold open — 8 min. Notes CLOSED.
1. *(S1)* The full %↔fraction table.
2. *(S2)* A in 12, B in 18 — LCM method?
3. *(S3)* Unit digit of 7^53? "At least one" — the fast route?

## ① A-10 · Series

**Anchor:** *"Check the gaps first. If the gaps don't work, check the ratios."*

**A fixed order of attack — run it every time, don't improvise:**

```
1. DIFFERENCES between terms       →  constant? arithmetic
2. DIFFERENCES of the differences  →  constant? quadratic-ish
3. RATIOS                          →  constant? geometric
4. squares / cubes ± small number
5. alternating — two series woven together
6. previous term × n ± k
```

```
2, 6, 12, 20, 30, ?       gaps: 4, 6, 8, 10 → next gap 12 → 42
                          (also n²+n: 2,6,12,20,30,42)

3, 6, 12, 24, ?           ratio 2 → 48

1, 4, 9, 16, ?            squares → 25

2, 3, 5, 7, 11, ?         primes → 13     ← always check primes

5, 11, 23, 47, ?          ×2 + 1 → 95
```

**Letter series** — convert letters to numbers immediately: `A=1 … Z=26`.
```
A, C, F, J, ?             1, 3, 6, 10 → gaps 2,3,4 → next gap 5 → 15 = O
```
**Worth memorising:** `A=1 E=5 J=10 O=15 T=20 Y=25`. Those five anchors let you place any letter in two seconds.

**The Gotcha:** if the differences look chaotic, **check alternate terms** — two interleaved series is the single most common "hard" series, and it collapses the moment you split it.

**Recall:** *Your fixed order of attack on a number series — first three steps?*

---

## ② A-11 · Coding–decoding

**Anchor:** *"Find the shift. It's almost always +1, −1, +2, or a reversal."*

```
TYPE 1 · letter shift
  CAT → DBU      each letter +1

TYPE 2 · reverse
  CAT → TAC

TYPE 3 · opposite letter (A↔Z, B↔Y …)
  CAT → XZG      A↔Z, C↔X, T↔G       trick: position + opposite = 27

TYPE 4 · word-to-number substitution
  "sky is blue" = "pa ni ru";  "sky is red" = "pa ni ta"
  → common words map to common codes. Match by elimination.

TYPE 5 · number code
  CAT → 3, 1, 20      just A=1..Z=26
```

**The Gotcha:** always check **the first letter first**. If the shift is +1 there, test it on the rest. Most questions are solved by that single check — trying to spot the whole pattern at once wastes the time.

**Recall:** *A↔Z opposite letters — what do the two positions always add up to?*

---

## ③ A-12 · Blood relations & directions

**Anchor:** *"Draw it. Never hold a family tree in your head."*

```
notation:      +  male       −  female
               ═  married    │  child of      ─  sibling

"A is B's father. B is C's sister. C is D's mother."

        A+
        │
    ┌───┴───┐
   B−       C
            │
            D
```

**The single move that solves the hard ones — read backwards:**
> *"The son of my mother's only brother"* — read it from the **end**:
> my mother → her only brother (my maternal uncle) → his son → **my cousin.**

Working backwards through the phrase turns a confusing sentence into a walk down the diagram.

**Directions** — draw the compass every single time:
```
        N
        │
   W ───┼─── E          right turn  = clockwise
        │                left turn  = anticlockwise
        S

Facing North, turn right → East. Turn right again → South.
```

**The Gotcha:** *"to his right"* depends on **which way he's facing**, not on the page. Redraw the person's facing direction after every turn — this is where almost all direction marks are lost.

**Recall:** *"Son of my mother's only brother" — how do you read it, and what's the answer?*

> ✍️ **Blank page, 4 min.** The 6-step series attack · the five coding types · the blood-relation notation.

---

## ⏱ SPEED DRILL — 14 questions, **40 seconds each**

```
 1.  3, 8, 15, 24, ?
 2.  1, 2, 6, 24, ?
 3.  2, 5, 10, 17, 26, ?
 4.  7, 14, 28, 56, ?
 5.  4, 9, 25, 49, 121, ?
 6.  B, D, G, K, ?
 7.  If CAT = DBU, then DOG = ?
 8.  If A=1, code for "MAT"?
 9.  Opposite letter of F?
10.  "pit na to" = "she is good", "na ko re" = "he is bad". Code for "is"?
11.  A is B's brother, B is C's daughter. A is C's ___?
12.  Pointing to a photo: "She is my father's only daughter." Who is she?
13.  Facing East, turn right, then left, then right. Now facing?
14.  Walk 5 km North, 3 km East, 5 km South. Distance from start?
```

<details><summary>Answers + shortcut</summary>

1. **35** — gaps 5,7,9 → 11
2. **120** — ×1, ×3, ×4… actually n! → 1,2,6,24,120
3. **37** — n²+1: 2,5,10,17,26,37
4. **112** — ×2
5. **169** — squares of primes 2,3,5,7,11,13
6. **P** — 2,4,7,11 gaps 2,3,4 → +5 = 16 = P
7. **EPH** — each +1
8. **13, 1, 20**
9. **U** — 6 + 21 = 27
10. **na** — common word in both = common code
11. **son** — B is C's daughter, A is B's brother → also C's child, male
12. **his sister** — *(unless the speaker is female; if a woman says it, herself)*
13. **East** — right→S, left→E, right→S… careful: E→right=S, S→left=E, E→right=S. **South**
14. **3 km** — north and south cancel
</details>

**Score:** correct __/14 · over 55 s → `mistakes.md`.

> Got #13 wrong? Almost everyone does. **Redraw the arrow after every single turn** — don't track it mentally.

## Ledger — 2 min
> Mark A-10, A-11, A-12. Tick S4.

---
---

# S5 · Syllogisms, puzzles, clocks, calendars

## ⓪ Cold open — 8 min. Notes CLOSED.
1. Your fixed order of attack on a number series.
2. Opposite letters — the two positions add to what?
3. *(S2)* Equal distances at 60 and 40 — average speed?

## ① A-13 · Syllogisms

**Anchor:** *"Draw the circles. Never reason in words."*

```
ALL A are B          SOME A are B         NO A are B
  ┌─────B─────┐       ┌──A──┐┌──B──┐       ┌──A──┐  ┌──B──┐
  │  ┌──A──┐  │       │    ╲╱     │        │     │  │     │
  │  └─────┘  │       │    ╱╲     │        └─────┘  └─────┘
  └───────────┘       └────┘└─────┘         separate, no touching
```

**The method — three steps, no shortcuts:**
```
1. Draw the given statements as circles.
2. Ask: is the conclusion true in EVERY possible drawing?
3. If you can draw even ONE arrangement where it fails → it does not follow.
```

**The four rules that settle most questions:**

| Given | Conclusion |
|---|---|
| All A are B | "Some B are A" **follows** · "All B are A" does **not** |
| Some A are B | "Some B are A" **follows** |
| No A are B | "No B are A" **follows** |
| Some A are not B | "Some B are not A" does **NOT** follow |

**Either–Or:** when two conclusions are individually uncertain but **together cover all cases**, the answer is *"either I or II follows."* Look for a complementary pair — *some/no* on the same terms.

**The Gotcha:** *"possibility"* questions flip the logic. *"All A being B is a possibility"* is true if you can draw it **even once** — not if it must always be true.

**Recall:** *"All A are B." Does "All B are A" follow? Does "Some B are A"?*

---

## ② A-14 · Puzzles, clocks, calendars

**Anchor (puzzles):** *"Start with the most restrictive clue, not the first one."*

```
Linear seating:     draw 5 blanks.  _ _ _ _ _
Circular:           draw the circle, mark facing-centre or facing-out FIRST
Floors:             draw a vertical ladder, top at the top
```

**The method:**
```
1. Read ALL clues before placing anything.
2. Start with the most DEFINITE clue ("C is at the extreme left"), never clue 1.
3. Pencil in only what's certain. Leave the rest blank.
4. Use elimination — the answer usually falls out.
```

**The skip rule:** a puzzle set is 4–5 questions on one arrangement. **If you can't fix a single position after 2 minutes, leave the whole set and come back.** Sunk cost destroys more OA scores than difficulty does.

---

**Clocks:**
```
minute hand:  6° per minute        hour hand:  0.5° per minute
angle = |30H − 5.5M|               (if > 180, subtract from 360)

3:40  →  |90 − 220| = 130°

hands overlap 22 times a day (not 24) · 11 times in 12 hours
gain of a "fast" clock: straight proportion
```

**Calendars:**
```
odd days = days left over after complete weeks

ordinary year = 1 odd day       leap year = 2 odd days
100 years = 5 · 200 = 3 · 300 = 1 · 400 = 0

leap year: ÷4, but century years only if ÷400   (1900 no, 2000 yes)
```

**The Gotcha:** the clock angle formula gives the *smaller* angle only if you subtract from 360 when it exceeds 180. And a "century year" is not automatically a leap year — 1900 wasn't.

**Recall:** *Angle at 3:40? Odd days in an ordinary year? Is 1900 a leap year?*

> ✍️ **Blank page, 4 min.** The three syllogism circles · the four rules table · the clock angle formula · odd days.

---

## ⏱ SPEED DRILL — 14 questions, **45 seconds each**

```
 1.  All cats are animals. All animals are living. → All cats are living?
 2.  All A are B. → Some B are A?
 3.  Some pens are books. → Some books are pens?
 4.  No X is Y. → No Y is X?
 5.  Some A are not B. → Some B are not A?
 6.  Angle between the hands at 3:00?
 7.  Angle at 4:20?
 8.  How many times do the hands overlap in 24 hours?
 9.  Odd days in a leap year?
10.  Is 2100 a leap year?
11.  Odd days in 100 years?
12.  Five people in a row. C is at the extreme left, D at the extreme right,
     A is immediately right of C. Where can B and E be?
13.  If 1 Jan 2024 is a Monday, what day is 1 Jan 2025?
14.  Six friends around a circle facing centre. Who is opposite position 2?
```

<details><summary>Answers + shortcut</summary>

1. **Yes** — chained "all" statements always transmit
2. **Yes** — some-conversion always holds for "all"
3. **Yes** — "some" is symmetric
4. **Yes** — "no" is symmetric
5. **No** — the classic trap. Draw it and you'll see it fail.
6. **90°** — |30(3) − 5.5(0)|
7. **10°** — |120 − 110|
8. **22** — not 24; they don't overlap between 11 and 12 twice
9. **2**
10. **No** — century year, and 2100 isn't divisible by 400
11. **5**
12. **positions 4 and 5, in either order** — C, A, _, _, D leaves two middle slots… careful: C _ _ _ D with A right of C → C A _ _ D → B and E fill slots 3 and 4
13. **Wednesday** — 2024 is a leap year → 2 odd days
14. **position 5** — in a circle of 6, opposite = +3
</details>

**Score:** correct __/14 · over 60 s → `mistakes.md`.

## Ledger — 2 min
> Mark A-13, A-14. Tick S5. **Reasoning done.** Next: `verbal.md`.
