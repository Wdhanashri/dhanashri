# Part 3 · SOLID & patterns — S8, S9, S10

**One session per sitting. ~70 min each.**

> These are **OOP interview questions**, not LLD. *"Explain SOLID"* and *"which design patterns do you know"* get asked in ordinary technical rounds, with no design problem attached. Splitwise gets finished in S10.

---
---

# S8 · SRP & OCP — the two that carry the weight

> Most guides dump all five SOLID letters on you with abstract definitions. You memorise five acronyms and can't apply any. **SRP and OCP do most of the real work** — they get this session; the other three get S9, framed as one idea, because that's what they are.

## ⓪ Cold open — 8 min. Notes CLOSED.
1. What does an ABC give you that duck typing doesn't?
2. What does polymorphism let you delete?
3. *(S6)* Does Python support method overloading?

## ① D-01 · Single Responsibility

**Anchor:** *"Can't describe the class without saying 'and'? It's two classes."*

That's the whole test. Say the job out loud:
```
"User stores name and email"                          ✅ one job
"User stores name and email AND sends emails AND
 validates passwords AND saves itself to the DB"      🚩 four jobs
```

Why it hurts, concretely:
```
change the email provider  → edit User
change MySQL to Mongo      → edit User
change password rules      → edit User
   three unrelated teams editing one file, breaking each other
```

```python
@dataclass
class User: name: str; email: str

class EmailService:      def send_welcome(self, u): ...
class UserRepository:    def save(self, u): ...
class PasswordValidator: def validate(self, pw) -> bool: ...
```

**Formal phrasing:** *"A class should have only one reason to change."* Then immediately give the test — the definition alone sounds memorised; the test proves you use it.

**The over-correction:** do **not** split until every class has one method. That makes fifty tiny classes nobody can follow. **One coherent responsibility, not one method.** `User` holding name, email *and* a balance is fine — that's all "being a user."

**Recall:** *The five-second test for a class doing too much?*

### 🔨 Find the "and"s — 6 min
```python
class Order:
    def calculate_total(self)          def apply_discount(self, code)
    def charge_card(self, card)        def send_confirmation_email(self)
    def generate_invoice_pdf(self)     def update_inventory(self)
```
> One sentence. Count the "and"s. Name the classes that should exist.

<details><summary>Check</summary>

`Order` (total, discount) · `PaymentProcessor` · `NotificationService` · `InvoiceGenerator` · `InventoryService`.

**`Order` keeps `calculate_total` and `apply_discount`** — both are genuinely "being an order." That's the over-correction warning in action.
</details>

---

## ② D-02 · Open/Closed

**Anchor:** *"Add a file, don't edit a file."*

> *Open for extension, closed for modification* — meaningless alone. Here's what it means:

```
NEW REQUIREMENT ARRIVES
  ❌ closed:  open PaymentProcessor.py, add an `elif`, re-test everything
  ✅ open:    create UpiPayment.py. Touch nothing else.
```

```python
class PaymentMethod(ABC):
    @abstractmethod
    def pay(self, amount: float) -> bool: ...

class CardPayment(PaymentMethod): ...
class UpiPayment(PaymentMethod):  ...      # NEW FILE. Nothing else touched.

def process(method: PaymentMethod, amount): return method.pay(amount)
```

**Why "don't edit" is the point:** editing working code means **re-testing working code**. Adding a class means testing only the new thing.

**Notice what OCP is made of:** an ABC plus polymorphism. **SOLID is not new material** — it's names for judgement you've been building since S6.

**The trap:** making everything extensible is abstraction soup. **Ask: "will there realistically be a version 2?"** No → leave it concrete.

**Recall:** *When a new requirement arrives, what does OCP let you avoid?*

> ✍️ **Blank page, 4 min.** The "and" test, the payments before/after, and why not editing matters.

## 🔨 Build it — 30 min · the big refactor

Create `splitwise/v2_solid.py`.
```python
# Something is doing too much — probably Group (members AND expenses AND
# balance updates AND validation). Split into:
#   Group             → membership only
#   BalanceSheet      → the ONLY thing that mutates balances
#   ExpenseValidator  → is this expense legal?
#   ExpenseService    → orchestrates: validate → split → update
# Each gets a ONE-SENTENCE docstring with no "and". Can't write it → split is wrong.
#
# THEN: add SharesSplit. You may create a new class. You may NOT edit an existing one.
#       Have to edit something? The design isn't open. Fix the design first.
```

**Acceptance:** one new class, zero edits. **Everything before this is theory until this passes.**

## 🎤 Out loud — 5 min
> **"What is the Open/Closed Principle? Give an example."** 2 min. **Always give an example** — SOLID answers without one sound memorised, because they usually are.

## Ledger — 2 min
> Mark D-01, D-02. Tick S8.

---
---

# S9 · L, I, D — and the warning that matters most

## ⓪ Cold open — 8 min. Notes CLOSED.
1. The five-second test for a bloated class.
2. What does OCP let you avoid?
3. *(S6)* Overriding to raise an error — what does it mean?

## ① D-03 · Depend on the promise

**Anchor:** *"Depend on the promise, not on the class that keeps it."*

L, I and D are three angles on one idea: **code against what something promises, never against what it concretely is.**

### L · Liskov Substitution
> *A subclass must be usable anywhere its parent is, without surprises.*

**You already know this** — S6's test 2, and the Penguin. `make_it_fly(Penguin())` crashes and the function did nothing wrong.

The canonical example, worth having ready:
```python
r = Rectangle(); r.width = 5; r.height = 4      # area 20
s = Square();    s.width = 5; s.height = 4      # area 16 — setting one
                                                # silently changed the other
```
Geometry says a square is a rectangle. **Code says no**, because Rectangle promised independent width and height.

### I · Interface Segregation
> *Don't force a class to implement methods it doesn't need.*
```python
class Worker(ABC):                    # 🚩 one fat interface
    @abstractmethod def work(self): ...
    @abstractmethod def eat(self): ...

class Robot(Worker):
    def eat(self): raise NotImplementedError    # 🚩 forced into nonsense
```
Split into `Workable` / `Eatable`. **The smell** — a subclass implementing a method with `pass` or `NotImplementedError` — is the *same* smell as an LSP violation. Two views of one mistake.

### D · Dependency Inversion — the one that changes your code
```python
class ExpenseService:                 # 🚩 welded to MySQL and Gmail
    def __init__(self):
        self.db = MySQLDatabase()
        self.mailer = GmailSender()
```
You now cannot test this without a live MySQL and a real Gmail account. **That's how untestable code is born.**

```python
class ExpenseService:                 # ✅ dependency injection
    def __init__(self, db: Database, mailer: Notifier):
        self.db, self.mailer = db, mailer

ExpenseService(MySQLDatabase(), GmailSender())   # production
ExpenseService(FakeDatabase(),  FakeMailer())    # tests, instantly
```

The whole thing is: **take it as a parameter instead of creating it inside.**

**Say this in an interview:** *"I'd inject the dependency so it's testable."* Short, signals real experience, and freshers almost never say it.

**Recall:** *Your class creates a `MySQLDatabase()` inside `__init__`. What's wrong, and what's the fix?*

> ✍️ **Blank page, 5 min.** All five SOLID letters with a **one-line test each** — no definitions, just the tests. Then the DI before/after.

### 🔨 Spot the violation — 6 min. Name the letter, then the fix.
```
1. ReportGenerator that formats, prints, emails and archives.
2. Ostrich(Bird) whose fly() raises NotImplementedError.
3. OrderService whose __init__ does self.payment = StripeGateway().
4. ABC Vehicle with fly(), sail(), drive() — Car implements all three.
5. A new discount type means editing a 60-line if/elif.
```
<details><summary>Check</summary>

1. **SRP** 2. **LSP** 3. **DIP** 4. **ISP** 5. **OCP** — 5/5 is the actual skill, not reciting acronyms.
</details>

---

## ② The warning that matters most

**KISS beats SOLID in a 45-minute interview.**

The most common way freshers fail a design round is **over-engineering** — bolting on a Factory and an Observer and four ABCs to look impressive. Interviewers read that as *"doesn't know when to stop."*

```
Start with the simplest thing that works.
Add an abstraction only when you can NAME the change it protects against.
```

Asked *"why didn't you use a Factory here?"*, be confident, not apologetic:
> *"There's only one kind of user right now, so a Factory would be indirection with no payoff. If we added a second type I'd introduce one."*

**That scores better than having built the Factory.**

## 🔨 Build it — 25 min
```python
# 1. ExpenseService.__init__(self, balance_sheet, validator, splitter, notifier=None)
#    Create TWO services — one real, one entirely fake.
#    Write FakeBalanceSheet that just records calls in a list.
#    Run the full flow with zero real components and assert what the fake recorded.
#      ← that's a unit test, written without a framework.
#
# 2. Read your own file with the 5 tests in hand. Find TWO violations. Write:
#      # VIOLATION (letter): what's wrong → how I'd fix it
#    Fix ONE. Leave the other with a note saying why it isn't worth fixing yet.
```

**Acceptance:** you left one deliberately unfixed, with a reason. **Knowing what not to fix is what this session teaches.**

## 🎤 Out loud — 5 min
> **All five SOLID principles, one sentence and one example each.** Time it. **Under 3 minutes** is the interview-usable version.

## Ledger — 2 min
> Mark D-03. Tick S9.

---
---

# S10 · Strategy & Factory — Splitwise finished

## ⓪ Cold open — 8 min. Notes CLOSED.
1. All five SOLID letters, one-line test each.
2. Your class creates `MySQLDatabase()` in `__init__` — what's wrong?
3. *(S7)* What does polymorphism let you delete?

## ① D-04 · Strategy

**Anchor:** *"`if type == ...` is a Strategy waiting to happen."*

**The most-cited pattern in interviews.** If you learn one, learn this.

> **The trigger:** any `if type == ...` or `switch(kind)` **choosing between behaviours**.

```python
class Splitter:                              # 🚩
    def split(self, kind, amount, users):
        if kind == "equal": ...
        elif kind == "exact": ...
```
```python
class SplitStrategy(ABC):                    # ✅
    @abstractmethod
    def split(self, amount, users) -> dict: ...

class ExpenseService:
    def __init__(self, strategy: SplitStrategy):
        self.strategy = strategy             # ← swap this, change everything
```

```
   ┌──────────────────┐     has-a      ┌──────────────────┐
   │  ExpenseService  │───────────────→│ SplitStrategy ABC│
   └──────────────────┘                └────────┬─────────┘
                                  ┌─────────────┼─────────────┐
                                  ▼             ▼             ▼
                                Equal         Exact        Percent
```

**You already built this in S6** — the swappable logger on `Service`. Meeting the mechanism before the name is why it should feel obvious.

| Problem | The Strategy |
|---|---|
| Parking Lot | pricing (hourly / flat) |
| Splitwise | split type |
| E-commerce | discount rules, shipping |

**Every one is "same job, different method."** That's the phrase to listen for.

---

## ② D-05 · Factory

**Anchor:** *"One place that knows how to build things."*

Strategy is about *behaviour*. Factory is about **creation**.

```python
class SplitFactory:
    @staticmethod
    def create(split_type: SplitType, **kwargs) -> SplitStrategy:
        if split_type == SplitType.EQUAL:   return EqualSplit()
        if split_type == SplitType.EXACT:   return ExactSplit(kwargs["amounts"])
        if split_type == SplitType.PERCENT: return PercentSplit(kwargs["percents"])
        raise ValueError(f"unknown split type: {split_type}")
```

**The honest bit: the if-chain didn't disappear — it moved.** And that's fine, because it now lives in exactly one place. Adding a type means editing one known file instead of hunting through four.

| | Strategy | Factory |
|---|---|---|
| About | **how** something is done | **which object** is created |
| Question | "which algorithm?" | "which class?" |

**They pair constantly:** a Factory *creates* the Strategy. That's your Splitwise.

**Recall:** *Strategy vs Factory — one sentence on the difference.*

> ✍️ **Blank page, 4 min.** The Strategy diagram, the trigger sentence, and the Strategy-vs-Factory contrast.

## 🔨 Build it — 35 min · **Splitwise, final**

Create `splitwise/final.py` — the thing you could walk through in an interview.
```python
#   Enums:    SplitType
#   Data:     User, Expense
#   Strategy: SplitStrategy ABC + Equal / Exact / Percent
#   Factory:  SplitFactory.create(split_type, **kwargs)
#   Core:     BalanceSheet (only thing that mutates balances)
#             Group (membership) · ExpenseService (injected dependencies)
#
# Must do: add users → group → add an expense with ANY split type chosen from a
#          STRING as if from input → show who owes whom → settle_up(a, b)
```

**Acceptance:** a demo with 3 users and 3 expenses using **3 different split types**, printing a correct balance sheet. Then add `SharesSplit` **without editing any existing class**.

> Write a short `DESIGN.md`: **Classes · Why Strategy · Why Factory · What I'd add next · What I deliberately left out and why.** That last section impresses — *"no Observer because nothing needs notifying yet"* beats an Observer nobody asked for.

## 🎤 Out loud — 6 min
1. **"Which design patterns do you know?"** 90 sec — Strategy, Factory, Observer, Singleton, one line each.
2. **Walk through your Splitwise design.** 3 min, timed.

## Ledger — 2 min
> Mark D-04, D-05. Tick S10. Next: `p4-interview.md`.
