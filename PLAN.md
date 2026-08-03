# The Plan — one table, one daily order, one rule when you slip

**This is the only file that answers "what do I do today?" across all five courses.**

Each course has its own decision tree. This sits above them.

---

## The idea this is built on

**A company might call you in week 5.** So the order is not "logical" — it's **most-asked first, cheapest first**.

```
asked in 100% of interviews, costs 4 hours   →  personal/     week 1
gates every service company, costs 9 hours   →  aptitude      weeks 2-3
~70% of all DSA questions asked              →  DSA Tier 1    weeks 1-4
the rest                                     →  after that
```

**By the end of week 4 you can walk into a service-company process and clear it end to end.** Everything after that is raising the ceiling, not reaching the floor.

---

## ① The table

**DSA is the anchor and never moves.** Everything else fits around it.

```
Mon–Sat   DSA          120 min    ← the anchor
3 days    2nd subject   75 min    ← rotates
Sun       rest, or catch up. Not both.
```

| Week | DSA (the anchor) | Second subject | Hrs |
|---|---|---|---|
| **1** | D1–D7 · arrays, hashing, two pointers | **`personal/`** — all 5 files | 16 |
| **2** | D8–D14 · sliding window, stack | `aptitude/` S1–S3 (quant) | 16 |
| **3** | D15–D21 · binary search, linked list | `aptitude/` S4–S6 | 16 |
| **4** | D22–D28 · trees · **Tier 1 exit gate** | `aptitude/` S7 ✅ · `cs-fund/` OS S1–S2 | 16 |
| **5** | D29–D35 · heap, backtracking | `cs-fund/` OS S3 ✅ · DBMS S1–S2 | 16 |
| **6** | D36–D42 · graphs, tries | `cs-fund/` DBMS S3 ✅ · CN S1–S2 | 16 |
| **7** | D43–D49 · Dijkstra, MST, math | `cs-fund/` CN S3 ✅ · `lld/` S1–S2 | 16 |
| **8** | D50–D56 · 1-D DP | `lld/` S3–S5 | 16 |
| **9** | D57–D63 · 2-D DP | `lld/` S6–S8 | 16 |
| **10** | D64–D70 · greedy, intervals, bit · **final gate** | `lld/` S9–S11 | 16 |
| **11** | maintenance only | `lld/` S12 ✅ · `hld.md` (one sitting) | 10 |
| **12+** | maintenance + mocks | — | 8 |

**~16 hours a week.** That's 2 hours of DSA six days a week, plus three 75-minute sessions. Alongside classes it's demanding, not impossible — and it's the number that finishes in twelve weeks instead of twenty.

---

## ② What you can survive, and when

**This is the honest version. Read it when you're wondering if you're ready.**

| After week | You can hold your own in | You cannot yet |
|---|---|---|
| **1** | An HR round. Intro, project, behavioural — all rehearsed. | Almost any coding round |
| **3** | An aptitude OA. Easy array/string/window problems. | Trees, graphs, DP |
| **4** ⭐ | **A full service-company process** — OA → DSA round → CS basics → HR. TCS, Infosys, Wipro, Accenture, Cognizant. | Product-company DSA rounds |
| **7** | A mid-tier product company. All CS fundamentals + Tier 1 + graphs. | DP-heavy rounds, LLD rounds |
| **10** | A good product company. All 150 problems, most of OOP/LLD. | Nothing structural |
| **11+** | Everything on your list. | — |

> **Week 4 is the milestone that matters.** If placements start early, that's the date to circle — not week 12.

---

## ③ The daily order

```
┌─ 1. LEDGER CHECK ─ 5 min ───────────────────────────────────┐
│ Open the ledger of BOTH live courses. Anything overdue?      │
│   YES → do those reviews first. They outrank new material.   │
└──────────────────────────────────────────────────────────────┘
┌─ 2. DSA ─ 120 min ──────────────────────────────────────────┐
│ Hardest thing you'll do. Do it when your head is freshest.   │
│ One day file, top to bottom. Stop at the cap even mid-problem│
└──────────────────────────────────────────────────────────────┘
┌─ 3. SECOND SUBJECT ─ 75 min, 3 days a week ─────────────────┐
│ Different part of your brain. Best in a separate sitting —   │
│ morning DSA, evening second subject, if you can split them.  │
└──────────────────────────────────────────────────────────────┘
```

**Never do DSA and LLD back to back when tired.** Both are high-load and the second one is wasted. Aptitude or CS fundamentals after DSA is fine — those are recall, not construction.

---

## ④ When you fall behind — and you will

**Follow this in order. Don't improvise it at 11pm when you feel bad.**

```
BEHIND 1-2 DAYS     drop the 🔵 stretch problems for that week.
                    That's what they're there for.

BEHIND ~1 WEEK      pause the second subject for one week.
                    DSA is the anchor; everything else can wait a week.

BEHIND 2+ WEEKS     cut Tier 2 SCOPE, not review. Keep:
                      heap · backtracking · graphs · 1-D DP · intervals
                    Drop:
                      advanced graphs · 2-D DP stretch · math & geometry
                    That keeps ~80% of what gets asked.

NEVER               cut the cold open. Not once, not for anything.
```

> **The cold open is the whole system.** Skipping review to cover more ground is exactly the trade that put you here — a bigger syllabus you've forgotten beats nothing. **Cut scope. Never cut review.**

---

## ⑤ An interview lands in three days

**Stop the plan. Do this instead.**

```
DAY -3 / -2   normal schedule, but replace new material with:
              · the rapid-fire file for whatever they'll ask
              · one timed mock (2 problems, 45 min, think-aloud, recorded)

DAY -1        NO NEW MATERIAL. None. It only shakes your confidence.
              · personal/intro.md — say it twice, out loud        10 min
              · dsa/anchors.md — the pattern-picker table         10 min
              · the relevant rapid-fire, out loud                 20 min
              · cartwise.md — 60-sec version + draw the diagram   10 min
              · open-source.md — the 2-minute version             10 min
              Then stop. Sleep properly. That's worth more than
              another hour of revision, and it isn't close.

DAY 0         Read the 3 anchors files. Nothing else.
```

**Which rapid-fire?**
```
service company        →  aptitude/cheatsheet.md
any technical round    →  cs-fundamentals/*/rapid-fire.md
product company        →  dsa/anchors.md + lld/rapid-fire.md
```

---

## ⑥ Why this order — the 20% that gets asked 80% of the time

If you only ever finished the shaded rows, you'd still clear most fresher processes:

| Priority | What | Why it's first |
|---|---|---|
| 🟩 **1** | `personal/` | Asked in **100%** of interviews. 4 hours. Nothing else has this ratio. |
| 🟩 **2** | Aptitude | Zero value at product companies, **total gatekeeper** at service ones. No human reads your resume until you clear it. |
| 🟩 **3** | DSA Tier 1 | Arrays, hashing, two pointers, window, stack, binary search, LL, trees ≈ **70%** of fresher DSA questions. |
| 🟩 **4** | CS fundamentals | Cheap marks. Finite, unchanging syllabus. Round 2 at product companies, round 1 at service ones. |
| 🟨 5 | OOP (LLD S1–S7) | The four pillars get asked constantly; the *design* half rarely does. |
| 🟨 6 | DSA Tier 2 | Raises your ceiling. Graphs and DP are what separate candidates at good companies. |
| ⬜ 7 | LLD design + HLD | Real, but the least-asked per hour at your level. |

**Rows 1–4 are ~45 hours.** That's the floor, and you hit it at the end of week 4.
**Rows 5–7 are the other ~135 hours.** That's the ceiling.

---

## ⑦ Four things you'll worry about — answered

**"Am I ready?"**
Check the table in ②. It's a date, not a feeling. Feelings about readiness are unreliable in both directions.

**"A company came early and I'm only in week 3."**
Then you go, and you use §⑤. An interview you're 60% ready for still teaches you more than a week of studying — and the feedback goes straight into your mistake books. **Never decline an interview because you don't feel ready.**

**"There's too much."**
There is 16 hours a week for twelve weeks. That's it. On any given day the answer is one ledger check, one DSA file, and sometimes one other session. **You never need to hold the whole thing in your head — that's what the ledgers are for.**

**"I'm behind and I want to skip the reviews to catch up."**
That's the exact instinct that cost you the last three attempts at NC150. §④ exists so the decision is already made, on a good day, in writing. **Follow it instead of re-deciding.**

---

## The one-line version

> **Anchor on DSA six days a week. Rotate one second subject. Never skip the cold open. Circle week 4.**
