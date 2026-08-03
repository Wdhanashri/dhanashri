# Quant — S1, S2, S3

**One session per sitting. ~75 min. Stop at the horizontal rule. No calculator, ever.**

---
---

# S1 · Percentages, profit, ratio, averages, interest

> Arithmetic is **60% of the numerical section**. If you only had one week, you'd spend it here.

## ① A-01 · Percentages ↔ fractions

**Anchor:** *"Don't calculate a percentage — recognise it as a fraction."*

**This table is the single highest-value thing in the whole course. Memorise it today.**

```
1/2 = 50%      1/6  = 16.67%     1/11 = 9.09%
1/3 = 33.33%   1/7  = 14.28%     1/12 = 8.33%
1/4 = 25%      1/8  = 12.5%      1/15 = 6.67%
1/5 = 20%      1/9  = 11.11%     1/16 = 6.25%
                1/10 = 10%        1/20 = 5%
```

**Why it wins:** *"Find 37.5% of 256."* Long way: `256 × 37.5 / 100`. Fast way: **37.5% = 3/8**, so `256/8 × 3 = 96`. Two seconds.

**Successive percentage change** — memorise this one formula:
```
net change = a + b + (a×b)/100

  +20% then −20%   →  20 − 20 − 400/100  =  −4%     ← NOT zero. This is the trap.
  +10% then +10%   →  10 + 10 + 100/100  =  +21%
```

**Percentage increase vs decrease — the asymmetry:**
```
increase by 25%  →  multiply by 5/4
to undo it       →  decrease by 20%  (÷ 5/4), NOT 25%

"A is 25% more than B"  →  B is 20% less than A
```

**The Gotcha:** *more than* and *less than* are never symmetric. If A is 50% more than B, B is 33.33% less than A. Interviewers and OAs love this exact trap.

**Recall:** *What fraction is 12.5%? And +30% then −30% gives what net change?*

> ✍️ **Blank page, 3 min.** Write the whole fraction table from memory. Then the successive-change formula.

---

## ② A-02 · Profit & Loss

**Anchor:** *"Everything is a percentage of Cost Price — except discount, which is off Marked Price."*

```
CP ──profit%──► SP        Profit% = (SP − CP)/CP × 100     ← ALWAYS on CP
MP ──discount%──► SP      Discount% = (MP − SP)/MP × 100   ← ALWAYS on MP
```

| Situation | Shortcut |
|---|---|
| Profit x% | `SP = CP × (100+x)/100` |
| Loss x% | `SP = CP × (100−x)/100` |
| Two successive discounts | same successive formula: `a + b + ab/100` (both negative) |
| Sold two items, same SP, one at +x%, one at −x% | **always a loss** of `x²/100 %` |
| False weight (sells 900g as 1kg) | `gain% = error/(true value − error) × 100` |

**The classic:** *"Sells two articles at ₹1000 each, one at 20% profit, one at 20% loss. Net?"*
→ **Always a loss**, of `20²/100 = 4%`. Don't compute — recognise it.

**The Gotcha:** profit is on CP, discount is on MP. Mixing them up is the most common wrong answer, and the paper *knows* that — the wrong option is always there waiting.

**Recall:** *Same SP, one at +20%, one at −20% — profit or loss, and how much?*

---

## ③ A-03 · Ratio & mixtures

**Anchor:** *"Turn the ratio into parts, find one part, multiply."*

```
A : B = 3 : 5,  total = 40
                          3 + 5 = 8 parts,  40/8 = 5 per part
                          A = 15, B = 25
```

**Alligation — for any mixture question, use the cross:**
```
        cheap(20)          dear(30)
              ╲            ╱
                mean(24)
              ╱            ╲
      30−24 = 6        24−20 = 4

       cheap : dear  =  6 : 4  =  3 : 2
```
Works for prices, milk-water, alcohol, average marks — **anything with two groups and a weighted middle.**

**Recall:** *Milk at ₹20/l and ₹30/l mixed to sell at ₹24 — what ratio?*

---

## ④ A-04 · Averages

**Anchor:** *"Average × count = total. Always convert to total first."*

```
avg of 10 numbers = 25          → total = 250
one number 30 is replaced by 50 → total = 270 → new avg = 27

shortcut: change in avg = change in total / count = 20/10 = +2
```

| Pattern | Shortcut |
|---|---|
| Average of 1..n | `(n+1)/2` |
| Average of first n even numbers | `n+1` |
| Adding a person changes the average by d | new person = old average + `d × (new count)` |

**The Gotcha:** *"average speed"* is **never** the average of the two speeds. That's A-06.

**Recall:** *Average of 10 numbers is 25; one number 30 is replaced by 50. New average — without recomputing the total?*

---

## ⑤ A-05 · Simple & Compound Interest

**Anchor:** *"SI is on the original. CI is on the growing pile."*

```
SI = P·R·T/100
CI:  A = P(1 + R/100)^T,   CI = A − P

difference for 2 years:   CI − SI = P(R/100)²        ← memorise this
difference for 3 years:   CI − SI = P(R/100)²(3 + R/100)
```

**CI shortcut via successive percentages:** 10% for 2 years = `10 + 10 + 100/100` = **21%**. No powers needed.

**The Gotcha:** if interest is compounded **half-yearly**, rate halves and time doubles: `R/2`, `2T`.

**Recall:** *CI − SI for 2 years on ₹5000 at 10% — what's the formula, and the answer?*

> ✍️ **Blank page, 4 min.** The fraction table (again), the successive formula, the alligation cross, and `CI − SI = P(R/100)²`.

---

## ⏱ SPEED DRILL — 12 questions, **45 seconds each**. Timer on. Paper only.

```
 1.  62.5% of 320 = ?
 2.  Price rises 20% then falls 20%. Net change?
 3.  A is 25% more than B. B is what % less than A?
 4.  CP ₹400, sold at 15% profit. SP?
 5.  Successive discounts 20% and 10% = single discount of?
 6.  Two items sold at same SP, +25% and −25%. Net?
 7.  A:B = 2:3, B:C = 4:5. A:B:C = ?
 8.  Milk ₹15/l and ₹25/l mixed at ₹18/l. Ratio?
 9.  Average of 5 numbers is 20. One number 15 replaced by 35. New average?
10.  Average of first 20 natural numbers?
11.  SI on ₹8000 at 12% for 3 years?
12.  CI − SI, 2 years, ₹10000 at 5%?
```

<details><summary>Answers + the shortcut for each</summary>

1. **200** — 62.5% = 5/8 → 320/8 × 5
2. **−4%** — 20 − 20 − 400/100
3. **20%** — 25% more = ×5/4, undo = ÷5/4 = −20%
4. **₹460** — 400 × 115/100
5. **28%** — −20 −10 + 200/100 = −28
6. **loss of 6.25%** — x²/100 = 625/100
7. **8:12:15** — make B common: 2:3 = 8:12, 4:5 = 12:15
8. **7:3** — cross: (25−18):(18−15) = 7:3
9. **24** — total +20, so avg +20/5 = +4
10. **10.5** — (n+1)/2
11. **₹2880** — 8000 × 12 × 3/100
12. **₹25** — P(R/100)² = 10000 × (1/20)² = 25
</details>

**Score:** correct __/12 · anything over 60 seconds → `mistakes.md`, tagged.

## Ledger — 2 min
> Mark A-01 to A-05. Tick S1.

---
---

# S2 · Speed, distance, work

## ⓪ Cold open — 8 min. Notes CLOSED.
1. Write the full %↔fraction table.
2. +30% then −30% = ?
3. Two items at same SP, +10% and −10% — profit or loss, how much?
4. The alligation cross for ₹20 and ₹30 mixed at ₹26.

> Mark ✅/⚠️/❌. ❌ → 🔴 in `ledger.md`.

## ① A-06 · Time, Speed, Distance

**Anchor:** *"Distance fixed → speed and time are inversely proportional."*

```
D = S × T          km/hr → m/s :  × 5/18
                   m/s → km/hr :  × 18/5
```

**The inverse-ratio trick — this solves half the questions instantly:**
```
speeds in ratio 3:4  →  times in ratio 4:3   (same distance)

"walking at 3/4 speed he is 20 min late"
  → time ratio 4:3, so the EXTRA time (1 part) = 20 min
  → usual time = 3 parts = 60 min
```

**Average speed — never the plain average:**
```
equal DISTANCES at x and y:      2xy/(x+y)      ← harmonic mean
equal TIMES at x and y:          (x+y)/2

60 and 40 for equal distance → 2(60)(40)/100 = 48, NOT 50
```

**Relative speed — trains, boats, all the same idea:**

| Situation | Speed to use |
|---|---|
| Same direction | `a − b` |
| Opposite directions | `a + b` |
| Train crossing a pole | length of train |
| Train crossing a platform | train + platform |
| Boat downstream | `boat + stream` |
| Boat upstream | `boat − stream` |
| Given up & down speeds | `boat = (d+u)/2` · `stream = (d−u)/2` |

**The Gotcha:** a train crossing a *pole* covers only its own length. Crossing a *platform* covers train + platform. Reading too fast here costs the mark.

**Recall:** *Equal distances at 60 and 40 km/h — average speed? And why isn't it 50?*

---

## ② A-07 · Time & Work

**Anchor:** *"Make total work the LCM. Then everyone has a whole-number rate."*

**Forget fractions. Use LCM — it turns every work problem into simple arithmetic.**

```
A does it in 12 days, B in 18 days.  Together?

  total work = LCM(12, 18) = 36 units
  A's rate = 36/12 = 3 units/day
  B's rate = 36/18 = 2 units/day
  together = 5 units/day  →  36/5 = 7.2 days
```

No `1/12 + 1/18` anywhere. **This method is faster, and it makes every variant easy:**

| Variant | With LCM units |
|---|---|
| A and B together, A leaves after 4 days | subtract A's 4×3 units, B finishes the rest |
| Pipes filling / emptying | emptying pipe = **negative** rate |
| Efficiency: A is twice as fast as B | rates 2:1 → days 1:2 |
| M men in D days → M₁D₁ = M₂D₂ | direct proportion |

**Pipes** are identical to work — a leak is just a worker with a negative rate.

**The Gotcha:** *"A is twice as efficient as B"* means A's **rate** is double, so A takes **half** the days. Rate and time are inverses; swapping them is the standard trap.

**Recall:** *A in 10 days, B in 15 days. Using LCM, what's the total work and each rate?*

> ✍️ **Blank page, 4 min.** The average-speed formulas, the relative-speed table, and the LCM work method.

---

## ⏱ SPEED DRILL — 12 questions, **50 seconds each**

```
 1.  72 km/hr in m/s?
 2.  Equal distances at 30 and 60 km/h. Average speed?
 3.  Speeds ratio 5:6. Time ratio?
 4.  Walking at 3/4 of usual speed, 15 min late. Usual time?
 5.  Train 150 m at 54 km/h crosses a pole in?
 6.  Same train crosses a 300 m platform in?
 7.  Two trains, 60 and 40 km/h, opposite directions. Relative speed?
 8.  Boat: downstream 15, upstream 9 km/h. Boat speed? Stream?
 9.  A in 12 days, B in 24 days. Together?
10.  A in 20 days, works 5 days, leaves. B (30 days) finishes. B works how long?
11.  Pipe fills in 6 hr, leak empties in 12 hr. Time to fill?
12.  15 men, 8 days. 10 men take how many days?
```

<details><summary>Answers + shortcut</summary>

1. **20 m/s** — × 5/18
2. **40** — 2(30)(60)/90
3. **6:5** — inverse
4. **45 min** — time ratio 4:3, extra 1 part = 15, usual = 3 parts
5. **10 s** — 150 m at 15 m/s
6. **30 s** — 450 m at 15 m/s
7. **100 km/h** — opposite → add
8. **12 and 3** — (15+9)/2 and (15−9)/2
9. **8 days** — LCM 24: rates 2 and 1 → 3/day → 24/3
10. **22.5 days** — LCM 60: A=3, B=2. A does 15, remaining 45, /2
11. **12 hr** — LCM 12: +2, −1 → net 1/hr
12. **12 days** — 15×8 = 10×D
</details>

**Score:** correct __/12 · over 65 s → `mistakes.md`.

## Ledger — 2 min
> Mark A-06, A-07. Tick S2.

---
---

# S3 · Numbers, counting, data interpretation

## ⓪ Cold open — 8 min. Notes CLOSED.
1. Equal distances at 60 and 40 — average speed, and why not 50?
2. A in 12, B in 18 — LCM method, together?
3. *(S1)* 1/8 = ?% · 1/6 = ?% · successive +20/−20?

## ① A-08 · Numbers

**Anchor:** *"Divisibility, remainders and unit digits are all pattern-spotting, not arithmetic."*

**Divisibility rules — the ones that appear:**
```
2   last digit even          3   digit sum ÷ 3        4   last TWO digits ÷ 4
5   ends 0 or 5              6   ÷2 and ÷3            8   last THREE digits ÷ 8
9   digit sum ÷ 9            11  (odd-place sum) − (even-place sum) ÷ 11
```

**Unit digit of a power — cycles of 4:**
```
2 → 2,4,8,6   3 → 3,9,7,1   7 → 7,9,3,1   8 → 8,4,2,6
0,1,5,6 → always themselves.     4 → 4,6      9 → 9,1

7^53 :  53 mod 4 = 1  →  first in the cycle  →  7
```

**LCM & HCF:**
```
LCM × HCF = product of the two numbers
LCM of fractions  = LCM(numerators) / HCF(denominators)
HCF of fractions  = HCF(numerators) / LCM(denominators)

"smallest number leaving remainder r with each"  →  LCM + r
"largest number dividing a,b,c leaving same remainder"  →  HCF of the differences
```

**Squares and cubes to have instant:** squares 1–30, cubes 1–15, powers of 2 up to 2¹⁰ = 1024.

**Recall:** *Unit digit of 3^47? Rule for divisibility by 11?*

---

## ② A-09 · Permutations, combinations, probability

**Anchor:** *"Does order matter? P if yes, C if no."*

```
nPr = n!/(n−r)!          arrangements — ORDER matters
nCr = n!/(r!(n−r)!)      selections   — order does NOT

nCr = nC(n−r)     ← 10C8 = 10C2 = 45. Always take the smaller.
```

| Situation | Do this |
|---|---|
| Arrange n items | `n!` |
| n items, p alike | `n!/p!` |
| Circular arrangement | `(n−1)!` |
| Two people must sit together | glue them: `(n−1)! × 2` |
| At least one | `total − none` ← **almost always easier** |

**Probability:**
```
P(E) = favourable / total          0 ≤ P ≤ 1
P(not E) = 1 − P(E)                ← use this constantly
P(A or B)  = P(A) + P(B) − P(A and B)
P(A and B) = P(A) × P(B)    if independent
```

```
one die:  6      two dice:  36      one card:  52 (4 suits × 13, 26 red, 12 face)
```

**The Gotcha:** *"at least one"* almost always means **`1 − P(none)`**. Computing it directly means summing several cases and running out of time.

**Recall:** *"At least one head in 3 tosses" — what's the fast route?*

---

## ③ Data Interpretation — a technique, not a topic

**Anchor:** *"Read the question first, then look at the chart."*

DI is just percentages and ratios wearing a costume. The marks are lost to **method, not maths**:

```
1. Read the QUESTION before studying the chart.  ← most people do this backwards
2. Check the units. "in thousands", "in lakhs", "%" vs absolute.
3. Approximate. Options are usually far apart — 48.7% and 51% won't both be there.
4. Use the fraction table: "roughly a third" beats dividing to two decimals.
```

**The Gotcha:** a DI set is 4–5 questions on one chart. **Understand the chart once, and all five become fast.** Skipping the whole set because question 1 looked hard throws away four easy marks.

> ✍️ **Blank page, 4 min.** Divisibility rules for 4, 8 and 11 · the unit-digit cycles for 2, 3, 7, 8 · nCr = nC(n−r) · the four DI steps.

---

## ⏱ SPEED DRILL — 12 questions, **50 seconds each**

```
 1.  Is 3,08,352 divisible by 8?
 2.  Unit digit of 7^53?
 3.  Unit digit of 2^40?
 4.  Is 918082 divisible by 11?
 5.  HCF of two numbers is 6, LCM is 36. One is 12. The other?
 6.  Smallest number leaving remainder 3 when divided by 4, 6 and 8?
 7.  In how many ways can the letters of LEVEL be arranged?
 8.  10 people, choose 3?
 9.  8 people around a round table?
10.  Probability of at least one head in 3 coin tosses?
11.  Two dice — probability the sum is 8?
12.  One card drawn — probability it's a red face card?
```

<details><summary>Answers + shortcut</summary>

1. **Yes** — last three digits 352 ÷ 8 = 44
2. **7** — 53 mod 4 = 1 → cycle 7,9,3,1 → 7
3. **6** — 40 mod 4 = 0 → last in cycle 2,4,8,6
4. **Yes** — (9+8+8) − (1+0+2) = 25 − 3 = 22 ✓
5. **18** — LCM × HCF = product → 36×6/12
6. **27** — LCM(4,6,8) = 24, +3
7. **30** — 5!/(2!×2!) for two L and two E
8. **120** — 10C3
9. **5040** — (8−1)!
10. **7/8** — 1 − P(no heads) = 1 − 1/8
11. **5/36** — (2,6)(3,5)(4,4)(5,3)(6,2)
12. **3/26** — 6 red face cards / 52
</details>

**Score:** correct __/12 · over 65 s → `mistakes.md`.

## Ledger — 2 min
> Mark A-08, A-09. Tick S3. **Quant done.** Next: `reasoning.md`.
