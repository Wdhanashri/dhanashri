# Part 4 · The interview — S11, S12

**Two sessions. This is the only LLD in the course, and that is deliberate.**

> **Why so little.** At fresher level you get *one* design question, at *basic* difficulty, and the interviewer is checking that you can name sensible classes and justify one pattern. Meanwhile you'll be asked about `self`, generators, decorators, the four pillars and SOLID in **every single round**. Time spent there pays about five times more. One guided design plus one timed attempt is genuinely enough.

---
---

# S11 · Observer, and the 6-step method

## ⓪ Cold open — 8 min. Notes CLOSED.
1. Strategy vs Factory — one line.
2. All five SOLID letters, one-line test each.
3. *(S4)* classmethod vs staticmethod. *(S3)* What is the GIL?

## ① D-06 · Observer (and the truth about Singleton)

**Anchor:** *"Don't call me — subscribe, and I'll call you."*

```python
class ExpenseService:                    # 🚩
    def add_expense(self, e):
        self._save(e)
        EmailService().send(e)           # now knows about email
        Analytics().track(e)             # ...and analytics
        AuditLog().write(e)              # ...and auditing
```
Every new "also do this" means editing it (**OCP violation**) and it now has four jobs (**SRP violation**).

```python
class Subject:
    def __init__(self): self._observers = []
    def subscribe(self, o): self._observers.append(o)
    def notify(self, event, data):
        for o in self._observers: o.update(event, data)

class ExpenseService(Subject):
    def add_expense(self, e):
        self._save(e)
        self.notify("expense_added", e)     # ← one line. Forever.
```

```
                ┌──────────────────┐
                │  ExpenseService  │
                └────────┬─────────┘
          ┌──────────────┼──────────────┐
          ▼              ▼              ▼
    EmailNotifier   Analytics       AuditLog
    ExpenseService knows NONE of their names.
```

**The trigger:** *"when X happens, tell A, B and C"* — especially when you don't know up front who'll care.

### Singleton — and why to be careful

Every fresher name-drops it. The honest version:

```python
class ParkingLot:
    _instance = None
    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
        return cls._instance
```
*(In Python a module is already a singleton — `settings = Settings()` in `config.py` is usually enough.)*

**The problems:** global state · untestable (tests share one instance) · **hides dependencies** — which directly contradicts S9's dependency injection.

**What to say:**
> *"I'd make ParkingLot a singleton since there's one physical lot — but I'd inject it rather than calling `getInstance()` everywhere, so it stays testable."*

**Much better than "I used Singleton because there's only one"** — which invites a follow-up most candidates can't handle.

**Recall:** *What phrase means "use Observer"? Two honest problems with Singleton?*

> ✍️ **Blank page, 4 min.** The `Subject` class from memory, plus the Observer trigger phrase.

### 🔨 Build it — 12 min
```python
# Add to final.py:
#   Observer ABC with update(event, data)
#   Subject with subscribe / unsubscribe / notify
#   ExpenseService extends Subject
#   EmailNotifier (prints) · ActivityLogger (appends to a list)
# Demo: subscribe both, add an expense, both fire.
#       Unsubscribe email, add another, only the logger fires.
```
**Acceptance:** `ExpenseService` contains the word "Email" **nowhere**. Search and check.

---

## ② L-01 · The 6-step method

**Anchor:** *"Clarify → nouns → verbs → relationships → code → extend."*

```
1. CLARIFY   3 questions. Scope, scale, edge cases.   3 min
2. NOUNS     List the entities.                       3 min
3. VERBS     What can each do? → methods.             3 min
4. RELATE    has-a? is-a? Draw the boxes.             5 min
5. CODE      Core flow first. Working > complete.    25 min
6. EXTEND    "What if we needed X?"                   5 min
```

**The trap: starting at step 5.** Under pressure everyone wants to type immediately. Steps 1–4 take twelve minutes and are **where most of the marks are** — the interviewer is watching *how you think*, and 1–4 is the only place that's visible.

**Step 1 — always ask.** Silence reads as "doesn't gather requirements."
```
Scope:  "Multiple floors, or one level?"
Scale:  "Roughly how many? Does that change the design?"
Edges:  "What if it's full? Do we handle payment?"
```
Then **state your assumptions out loud** and move.

**Step 5 — priority:** happy path working end to end → one extension point → edge cases if time remains. **A working small design beats a half-finished grand one. Every time.**

**Step 6 — pre-empt the follow-up.** Before they ask: *"If we needed weekend pricing, I'd add a `WeekendPricing` strategy — no existing class changes."* You've answered the next question and shown OCP without saying "OCP."

**Recall:** *Name the 6 steps in order.*

> ✍️ **Blank page, 3 min.** All 6 steps with time budgets, plus the three clarifying questions.

## 🔨 Parking Lot — 35 min, guided

**This is the "Hello World" of design questions.** One is enough — the shape transfers.

**Steps 1–4, on paper, 10 min. No keyboard.**
```
CLARIFY  → assume 3 floors · motorcycle/car/bus · hourly pricing that may change
           · reject when full · calculate the fee, don't process payment
NOUNS    → ParkingLot · ParkingFloor · ParkingSpot · Vehicle · Ticket · PricingStrategy
           (not Time, not Fee — those are values, not objects)
VERBS    → park · unpark · find_free_spot · assign/release · calculate
RELATE   →
     ParkingLot ── has-a ──→ list[ParkingFloor]
                └─ has-a ──→ PricingStrategy      ← swappable
     ParkingFloor ── has-a ──→ list[ParkingSpot]
     ParkingSpot  ── has-a ──→ Vehicle | None
     Vehicle      ← is-a ──  Motorcycle · Car · Bus
```

**Everything is has-a except `Vehicle`.** Normal, and exactly what S6 predicted.

| Decision | Why |
|---|---|
| `PricingStrategy` injected | pricing changes often — the obvious extension point |
| `Vehicle` uses inheritance | Car IS A Vehicle, removes nothing → passes both tests |
| `Ticket` is its own class | time + spot + vehicle always travel together |
| **No Factory** | three vehicle types created in one place — **indirection with no payoff** |

**Say that last row out loud in an interview.** Restraint scores.

**Step 5 — code it, 25 min.** `parking_lot.py`:
```python
# VehicleSize(Enum) · Vehicle(ABC) → Motorcycle/Car/Bus
# @dataclass ParkingSpot: spot_id, size, vehicle=None
#     is_free(), can_fit(v), assign(v), release()
# ParkingFloor: find_free_spot(size)
# @dataclass Ticket: id, vehicle, spot, entry_time → duration_hours()
# PricingStrategy(ABC) → HourlyPricing · FlatRatePricing   (NO if-chain)
# ParkingLot(floors, pricing)   ← both injected
#     park(v) -> Ticket   (raise ParkingFullError)
#     unpark(ticket) -> float · availability() -> dict
```
**Acceptance:** park 3 vehicles, print availability, unpark one with a fee, park again into the freed spot. Then swap `HourlyPricing` for `FlatRatePricing` **without editing `ParkingLot`**.

**Step 6 — 5 min, in comments.** Design answers only, no code:
1. *"What if we add EV spots with charging?"*
2. *"What if pricing differs on weekends?"*
3. *"What if we need a display board showing free spots?"*

<details><summary>Check</summary>

1. New `VehicleSize.EV` + spot type. If charging has behaviour, `ChargingSpot(ParkingSpot)` — check the is-a test first.
2. New `WeekendPricing(PricingStrategy)`. **Nothing else changes.** That's why pricing was a strategy from the start.
3. **Observer.** `ParkingLot` is the Subject, `DisplayBoard` subscribes. If you got this one, the first half of the session landed.
</details>

## 🎤 Out loud — 6 min
> **Present your Parking Lot design.** 4 min, timed, recorded. Questions → classes → relationships → why pricing is a Strategy → one extension.

## Ledger — 2 min
> Mark D-06, L-01. Tick S11.
>
> **S12 is the gate.** Don't prepare tonight — the ledger already did that, and cramming is the habit this system was built to break.

---
---

# S12 · GATE

**Do not read ahead. ~100 min. Phone in another room.**

## Part A · Blank page — 15 min

From memory, nothing open:
1. **All 23 anchors.** (Concept *names* from `rapid-fire.md` only if you go blank — never the anchors.)
2. **All five SOLID letters** with a one-line test each.
3. The **Strategy** diagram and the **6-step method**.
4. Write a **decorator** and an **ABC**, from scratch.

**Pass:** 18/23 anchors, both code shapes correct.

---

## Part B · Rapid fire — 25 min. Out loud. 60 seconds each.

**This is the bulk of the gate, because this is the bulk of a real interview.** Anything vague → `mistakes.md`.

```
PYTHON
 1. Mutable vs immutable — name three of each.
 2. Why does a mutable default argument keep its value?
 3. Shallow vs deep copy.
 4. `is` vs `==` — and when do you use `is`?
 5. Why can a tuple be a dict key but a list can't?
 6. `*args` vs `**kwargs`.
 7. When does `finally` run? When does `else`?
 8. `return` vs `yield`.
 9. Iterable vs iterator.
10. What is a decorator? Give the one-line equivalent of `@`.
11. What is the GIL, and when do threads still help?
12. What does `with` guarantee?

OOP
13. Explain `self`. What does `d.greet()` actually run?
14. Class variable vs instance variable — and the shared-list bug.
15. instance vs classmethod vs staticmethod.
16. `__str__` vs `__repr__`.
17. `__eq__` without `__hash__` — what breaks?
18. The four pillars, one line each.
19. What is encapsulation actually for?
20. Does Python have true private members?
21. Composition vs inheritance — the test.
22. Does Python support method overloading?
23. `class D(B, C)` — which method wins? How do you check?
24. What does polymorphism let you delete?
25. Abstract class vs interface — in Python.

DESIGN
26. All five SOLID letters with an example each.
27. Strategy vs Factory.
28. When would you use Observer?
29. Why is Singleton risky?
30. Biggest mistake freshers make in a design round?
```

**Pass:** 25 of 30 clean, no stall over 5 seconds.

<details><summary>Answers — only after you've said all 30</summary>

1. Immutable: int, str, tuple. Mutable: list, dict, set. 2. Created once at def time; the same object every call. 3. Shallow shares inner objects; deep copies all the way down. 4. `==` value, `is` identity — use `is` only for `None`. 5. Keys must be hashable = immutable. 6. Tuple of positionals / dict of keywords. 7. `finally` always; `else` only if no exception. 8. `return` ends, `yield` pauses and resumes. 9. Iterable has `__iter__`; iterator has `__next__` and remembers position. 10. A function that wraps another; `add = logged(add)`. 11. One thread runs Python bytecode at a time; threads still help I/O-bound work. 12. `__exit__` runs even on an exception.
13. `self` is the object left of the dot; `User.greet(d)`. 14. Class var is shared; a mutable one is shared by every instance. 15. `self` / `cls` / nothing — classmethod is for alternative constructors. 16. Friendly vs unambiguous; write `__repr__` if only one. 17. The object becomes unhashable — no sets, no dict keys. 18. Encapsulation, inheritance, polymorphism, abstraction. 19. Protecting an **invariant**. 20. No — `_` is convention, `__` is name mangling. 21. Say "A IS A B" out loud; sounds wrong → composition. 22. **No** — use default args, `*args`, or `singledispatch`. 23. B wins; check `D.__mro__`, left to right. 24. A type-checking if-chain. 25. No separate keyword — an ABC with only abstract methods is your interface.
26. SRP/OCP/LSP/ISP/DIP. 27. *How* it's done vs *which object* is created. 28. "When X happens, tell A, B and C." 29. Global state, untestable, hides dependencies. 30. **Over-engineering** — patterns nothing needed.
</details>

---

## Part C · One design, 35 min, timed, alone

**Notes closed. `rapid-fire.md` allowed for syntax only.**

> ### Design a Vending Machine.
> Products in slots. A user selects a slot, pays by cash or card, gets the product plus change. The machine tracks inventory and refuses when a slot is empty or payment is short. An admin can restock.

`vending_machine.py`. Follow the 6 steps: **10 min on paper, 20 coding, 5 on what-ifs.** **Stop at 35 minutes even if unfinished — interviews stop.**

**Then score yourself:**

| | Check | ✓ |
|---|---|---|
| 1 | 3+ clarifying questions written before any code | ☐ |
| 2 | Nouns and verbs listed before designing | ☐ |
| 3 | 4–7 classes — not 2, not 15 | ☐ |
| 4 | An `Enum` for a fixed set | ☐ |
| 5 | **Payment is a Strategy**, not an if-chain | ☐ |
| 6 | No class needs "and" to describe it | ☐ |
| 7 | Dependencies injected | ☐ |
| 8 | Custom exceptions | ☐ |
| 9 | Every class has `__repr__` | ☐ |
| 10 | The happy path **runs** | ☐ |
| 11 | You did **not** add a pattern nothing needed | ☐ |

<details><summary>A reference shape — compare, don't copy</summary>

```
Enums:      SlotStatus, PaymentType
@dataclass  Product(code, name, price) · Slot(slot_id, product, quantity)
ABC         PaymentStrategy → pay(amount), refund(amount)
              CashPayment (change) · CardPayment (no change)
class       Inventory → get_slot, restock, is_available
class       VendingMachine → inventory + payment strategy, INJECTED
              select(slot_id), insert_payment(amount), dispense(), cancel()
Exceptions: OutOfStockError, InsufficientPaymentError, InvalidSlotError
```

**Two things most people miss:** `Slot` as its own class (putting `quantity` on `Product` breaks when the same product is in two slots), and **`cancel()`** — refunding mid-transaction is the edge case interviewers reach for.
</details>

**Pass:** 8 of 11, and the happy path runs.

---

## Part D · Mistakes & ledger — 15 min

Re-solve every open row in `mistakes.md`, cold. Repeat failure → that concept drops to **🔴**.
Then mark all 23 concepts. Honestly — marking a shaky one 🟢 hides it from the only system that would have caught it.

---

## Scoring

| Result | Next |
|---|---|
| **All parts pass** | ✅ You can hold a Python + OOP round and answer a basic design question. Keep the weekly 10-minute recall. |
| **One part fails** | Only the failed concepts go back to the next session's row. Retest in 3 sessions. |
| **Two or more fail** | Two extra sessions: 🔴/🟡 only, plus redo Parking Lot from a blank file. |

**Never redo the whole course.** Re-reading what you passed is re-exposure with extra steps.

---

## Keeping it

- **Weekly, 10 min:** 5 concepts you haven't touched, cold.
- **Monthly, 30 min:** redesign Parking Lot or Splitwise from scratch.
- **Week before an interview:** all 23 anchors + the 30 rapid-fire questions, out loud.

---

> One sentence — what surprised you most that you'd forgotten?
>
> ________________________________________________

**Worth saying plainly.** Twelve sessions ago you could define encapsulation but couldn't write a class from scratch — that gap is where most people stay, because most courses teach definitions and never make you build anything.

You have a Splitwise, a Parking Lot and a Vending Machine here, all written by you, all running. In an interview you won't be recalling definitions. You'll be remembering things you built.
