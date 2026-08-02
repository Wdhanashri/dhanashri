# Ledger — Python · OOP · Design

**Open first, every session. Find your row. Do it. Close it.**

1. Recall each concept **from memory** — the anchor, then what it does. Only then check `rapid-fire.md`.
2. Mark: 🟢 fast · 🟡 slow · 🔴 blank.
3. **Anything 🔴 → write it into the next session's row by hand.** That's all the maths you do.

> Reviews are counted in **sessions**. At 3 a week the spacing lands where it should on its own.

---

## Recall calendar

| Session | File | Recall these first | Marks |
|---|---|---|---|
| S1 | `p1-python.md` | — | |
| S2 | `p1-python.md` | P-01 P-02 P-03 | |
| S3 | `p1-python.md` | P-01 · P-04 P-05 | |
| S4 | `p2-oop.md` | P-02 P-03 · P-06 P-07 | |
| S5 | `p2-oop.md` | P-04 P-05 · P-08 · O-01 O-02 | |
| S6 | `p2-oop.md` | P-01 · P-06 P-07 · O-03 O-04 | |
| S7 | `p2-oop.md` | P-08 · O-01 O-02 · O-05 O-06 O-07 | |
| S8 | `p3-design.md` | P-02 · O-03 O-04 · O-08 O-09 | |
| S9 | `p3-design.md` | P-07 · O-05 O-06 · D-01 D-02 | |
| S10 | `p3-design.md` | O-07 O-08 · D-01 D-02 · D-03 | |
| S11 | `p4-interview.md` | P-03 P-08 · O-02 O-09 · D-04 D-05 | |
| S12 | `p4-interview.md` | **GATE — all 23** | |

**After S12 — keep it alive.** Weekly, 10 minutes: pick 5 concepts you haven't touched, recall cold, mark them. Week before an interview: all 23 anchors + the 30 rapid-fire questions.

---

## Status board

**A concept is finished only after 🟢 twice in a row.**

### Python — 8
| | Concept | Status |
|---|---|---|
| P-01 | Mutable vs immutable | 🔴 |
| P-02 | What `=` copies · `is` vs `==` · deep copy | 🔴 |
| P-03 | Choosing list/tuple/set/dict · hashability | 🔴 |
| P-04 | `*args`/`**kwargs` · comprehensions · `sorted(key=)` | 🔴 |
| P-05 | Exceptions · custom exception classes · EAFP | 🔴 |
| P-06 | Generators & `yield` · iterable vs iterator | 🔴 |
| P-07 | Decorators | 🔴 |
| P-08 | The GIL · context managers | 🔴 |

### OOP — 9
| | Concept | Status |
|---|---|---|
| O-01 | `self` · `__init__` · class vs instance variables | 🔴 |
| O-02 | `@dataclass` · `Enum` · instance/class/static methods | 🔴 |
| O-03 | Dunders · `__str__` vs `__repr__` · operator overloading | 🔴 |
| O-04 | Encapsulation · invariants · `@property` | 🔴 |
| O-05 | Composition (has-a) | 🔴 |
| O-06 | Inheritance · `super()` · overriding vs overloading | 🔴 |
| O-07 | MRO & the diamond problem | 🔴 |
| O-08 | Polymorphism · duck typing | 🔴 |
| O-09 | ABC as a contract · abstract class vs interface | 🔴 |

### Design — 6
| | Concept | Status |
|---|---|---|
| D-01 | SRP — the "and" test | 🔴 |
| D-02 | OCP — add a file, don't edit one | 🔴 |
| D-03 | LSP · ISP · DIP | 🔴 |
| D-04 | Strategy | 🔴 |
| D-05 | Factory | 🔴 |
| D-06 | Observer (+ Singleton) | 🔴 |

### LLD — 1
| | Concept | Status |
|---|---|---|
| L-01 | The 6-step method | 🔴 |

---

## Build tracker

Tick when the code **runs**, not when it looks right.

| Session | Deliverable | ✅ |
|---|---|---|
| S1 | `splitwise/warmup.py` — copies, identity, hashability | ☐ |
| S2 | args/kwargs · multi-key sort · try/except/else/finally | ☐ |
| S3 | Generator · `@timer` decorator · `functools.wraps` | ☐ |
| S4 | `splitwise/v1_classes.py` — User, Expense, alt constructor | ☐ |
| S5 | Dunders · `@property` · the unhashable experiment | ☐ |
| S6 | Composition swap · `Split` hierarchy · MRO experiment | ☐ |
| S7 | If-chain deleted · `SplitStrategy` ABC · float trap | ☐ |
| S8 | `splitwise/v2_solid.py` — SRP split, new type without edits | ☐ |
| S9 | Dependency injection + fakes + two violations found | ☐ |
| S10 | **`splitwise/final.py`** + `DESIGN.md` | ☐ |
| S11 | Observer wired in · `parking_lot.py` | ☐ |
| S12 | `vending_machine.py` — solo, 35 min, cold | ☐ |
