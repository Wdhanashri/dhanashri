# Python · OOP · Design

**12 sessions. ~70 min each. 23 concepts. 6 files.**

At the end you can hold a Python + OOP technical round, and answer a basic design question.

---

## Where the time goes — and why

```
Python vocabulary   S1  S2  S3            ████████        25%
OOP mastery         S4  S5  S6  S7        ██████████      33%
SOLID & patterns    S8  S9  S10           ████████        25%
Design (LLD)        S11 S12               █████           17%
```

**This split is deliberate.** At fresher level you get *one* design question, at basic difficulty. But you'll be asked about `self`, generators, decorators, the four pillars and SOLID in **every single round**. So the weight sits where the questions are.

Everything here is something interviewers **actually ask**, in these words. Nothing is "useful background."

---

## Your 6 files

```
START-HERE.md      ← you are here
ledger.md          ← open first, every session
rapid-fire.md      ← anchors + 40 Q&A + syntax lookup. Your revision file forever.
mistakes.md        ← every wrong or vague answer

p1-python.md       S1  S2  S3     copies & identity · idioms · generators, decorators, GIL
p2-oop.md          S4  S5  S6  S7 classes · dunders · inheritance & MRO · polymorphism
p3-design.md       S8  S9  S10    SRP/OCP · L,I,D · Strategy + Factory → Splitwise done
p4-interview.md    S11 S12        Observer · 6-step method + Parking Lot · GATE

splitwise/         your code lives and grows here
```

**Each part file holds 3–4 sessions.** Do **one session per sitting** and stop at the horizontal rule. Never two in a day.

---

## The running project

From S4 you build **one thing**: a Splitwise clone. It starts ugly and ends as a clean, extensible design in S10 you could put on a whiteboard.

Every concept arrives *because the current code hurts* — never as a definition first.

> Most OOP courses teach the four pillars and leave you unable to write a class from scratch. That gap is why this course is shaped the way it is: **you write code in every single session.**

---

## The one decision tree

```
Anything OVERDUE in ledger.md?
        │
    YES ├──→ Do only those recalls. 15 min. Then stop or continue.
        │
    NO  └──→ Next session in your current part file. Top to bottom.
```

---

## When

**3 sessions a week, alongside DSA.** Finishes in ~4 weeks. Different part of your brain than DSA, so these slot into lighter days.

---

## The 5 rules

| # | Rule | Why |
|---|---|---|
| 1 | **Type every code block yourself.** Never copy-paste. | Your fingers learn syntax; your eyes don't. |
| 2 | **Blank page before notes.** Marked ✍️. | Reading feels like learning. Writing from memory *is*. |
| 3 | **Every 🔨 must actually run.** | "It looks right" is not the bar. |
| 4 | **70-minute cap.** Hard stop, even mid-exercise. | Finish next session. |
| 5 | **Say every answer out loud.** | This subject is tested verbally, 100% of the time. |

---

## The 23 concepts

| Part | Concepts |
|---|---|
| **Python** | P-01 mutable/immutable · P-02 copies & identity · P-03 containers · P-04 idioms · P-05 exceptions · P-06 generators · P-07 decorators · P-08 GIL & `with` |
| **OOP** | O-01 `self` & class vars · O-02 dataclass/Enum/method types · O-03 dunders · O-04 encapsulation · O-05 composition · O-06 inheritance · O-07 MRO · O-08 polymorphism · O-09 ABC |
| **Design** | D-01 SRP · D-02 OCP · D-03 LSP·ISP·DIP · D-04 Strategy · D-05 Factory · D-06 Observer |
| **LLD** | L-01 The 6-step method |

---

## What "done" looks like

- [ ] Answer 25 of the 30 rapid-fire questions cleanly, out loud
- [ ] Write a decorator, an ABC and a `@property` from a blank file
- [ ] Explain all four pillars and all five SOLID letters with examples, under 3 minutes each
- [ ] Turn a basic design problem into 4–6 sensible classes in 35 minutes
- [ ] Justify one pattern — **and one you deliberately didn't use**

That last line matters. **Over-engineering is the most common way freshers fail a design round.**

---

## The thing to hold on to

You already do this in DSA: look at a problem and ask *"which pattern is this?"*

OOP is the same skill, different question: **"what are the things here, and what does each one know?"**

**Now open `ledger.md`, then `p1-python.md`.**
