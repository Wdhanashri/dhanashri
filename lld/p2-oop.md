# Part 2 · OOP mastery — S4, S5, S6, S7

**One session per sitting. ~70 min each. Stop at the horizontal rule.**

> This is the heart of the course. **OOP questions appear in essentially every fresher technical round** — far more often than LLD does. Everything here gets asked out loud.

You'll build one thing across S4–S10: a **Splitwise clone**.

---
---

# S4 · Classes, and the three kinds of method

## ⓪ Cold open — 8 min. Notes CLOSED.
1. What's the difference between `return` and `yield`?
2. `@logged` — what one line is it equivalent to?
3. *(S1)* Why can a tuple be a dict key but a list can't?

## ① O-01 · `self`, `__init__`, and class vs instance variables

**Anchor:** *"`self` is whoever the method was called on."*

Every tutorial says "self refers to the instance" and moves on. That explains nothing. **This does:**

```python
class User:
    def __init__(self, name):
        self.name = name
    def greet(self):
        print(f"hi, {self.name}")

d = User("Dhanashri")
d.greet()               # what you write
User.greet(d)           # what Python ACTUALLY runs   ← same thing
```

**Run both. Same output.**

```
d.greet()
│
└─ Python rewrites this as →  User.greet(d)
                                       │
                                       └─ lands in the parameter named `self`
```

That's the whole mystery. `self` is an **ordinary parameter**, filled with the object on the left of the dot. `def greet(banana)` is legal Python and works — `self` is a convention, not a keyword.

**`__init__` is not a constructor.** Python creates the object, *then* hands it over:
```
1. Python makes an empty User object
2. Python calls  User.__init__(that_object, "Dhanashri")
3. your code sets self.name
```
Which is why it **returns nothing**. `return self` inside it is a `TypeError`.

### Class vs instance variables — asked directly

```python
class Dog:
    species = "Canis"          # CLASS variable — one copy, shared by all
    def __init__(self, name):
        self.name = name       # INSTANCE variable — one per object

a, b = Dog("Rex"), Dog("Bruno")
Dog.species = "X"              # changes it for BOTH
a.species = "Y"                # creates an INSTANCE variable on `a` only,
                               # shadowing the class one. b is unaffected.
```

**The gotcha, and it's the same bug as S1's default argument:**
```python
class Cart:
    items = []                 # 🚩 SHARED by every cart ever created
    def __init__(self):
        self.items = []        # ✅ each cart gets its own
```

**Recall:** *`d.greet()` — what does Python actually run? And what's the mutable-class-variable bug?*

> ✍️ **Blank page, 4 min.** Both call forms; the three steps of `User("x")`; the shared-list bug and its fix.

---

## ② O-02 · `@dataclass`, `Enum`, and the three method types

**Anchor:** *"`@dataclass` writes the boring code; `Enum` stops the typos."*

```python
@dataclass
class Expense:
    amount: float
    paid_by: str
    tags: list[str] = field(default_factory=list)   # NEVER = []
```
Free: `__init__`, `__repr__`, `__eq__`. **Write `__init__` by hand only when there's real logic in it** — validation, computed fields.

```python
class SplitType(Enum):
    EQUAL = "equal"

SplitType.EQAUL      # AttributeError immediately
"eqaul"              # silently wrong, debug it at 2am
```

### The three method types — a guaranteed question

```python
class User:
    count = 0

    def greet(self):                        # INSTANCE — needs the object
        return f"hi {self.name}"

    @classmethod
    def from_string(cls, s):                # CLASS — gets the CLASS as `cls`
        return cls(*s.split(","))           #   ← alternative constructor

    @staticmethod
    def is_valid_email(e):                  # STATIC — gets nothing.
        return "@" in e                     #   just lives here for tidiness
```

| | First arg | Can touch | Typical use |
|---|---|---|---|
| instance | `self` | this object | normal behaviour |
| `@classmethod` | `cls` | the class | **alternative constructors**, counters |
| `@staticmethod` | — | nothing | a helper that belongs here logically |

**The answer they want:** *"`classmethod` gets the class, so it's how you write an alternative constructor. `staticmethod` gets nothing — it's a plain function that lives in the class for organisation."*

**Recall:** *classmethod vs staticmethod — what does each receive, and what's classmethod actually for?*

## 🔨 Build it — 25 min · Splitwise v1

Create `splitwise/v1_classes.py`.

```python
# class User:
#   __init__(user_id, name, email) → also self.balances = {}
#   __repr__
#   add_balance(other_id, amount)  → += into the dict, create key if missing
#   total_owed() -> float          → sum of only POSITIVE balances
#   @classmethod from_csv("id,name,email") -> User      ← alt constructor
#   @staticmethod is_valid_email(e) -> bool
#   class variable: count — incremented in __init__
#
# class Expense:
#   __init__(id, amount, paid_by: User, participants: list[User], description="")
#       → raise ValueError if amount <= 0
#       → raise ValueError if paid_by not in participants
#   __repr__
#   split_equally() -> dict[str, float]
#
# Then: 3 users (one built via from_csv), one ₹900 expense paid by A split 3 ways.
#       B and C each owe A ₹300. Print all three users and User.count.
```

**Acceptance:** amount `0` raises. A payer outside the participants raises. `User.count` is 3. Both crashes happen *before* bad data is stored.

## 🎤 Out loud — 6 min
1. **"Explain `self` to someone who's never written a class."** 2 min — use `d.greet()` → `User.greet(d)`.
2. **"Instance vs class vs static method?"** 90 sec.

## Ledger — 2 min
> Mark O-01, O-02. Tick S4.

---
---

# S5 · Dunders & encapsulation

## ⓪ Cold open — 8 min. Notes CLOSED.
1. `d.greet()` — what does Python actually run?
2. classmethod vs staticmethod — what does each receive?
3. *(S1)* The mutable-default trap. *(S3)* What is a decorator?

## ① O-03 · Dunders and operator overloading

**Anchor:** *"Define the dunder and Python's own syntax starts working on your class."*

When you write `len(x)` Python runs `x.__len__()`. When you write `a + b` it runs `a.__add__(b)`. **Those dunders are how your class plugs into the language.**

```python
@dataclass
class Money:
    amount: float
    currency: str = "INR"

    def __str__(self):  return f"₹{self.amount:.2f}"        # for HUMANS
    def __repr__(self): return f"Money({self.amount!r})"     # for DEVELOPERS
    def __add__(self, other): return Money(self.amount + other.amount)
    def __lt__(self, other):  return self.amount < other.amount
    def __eq__(self, other):  return self.amount == other.amount
    def __hash__(self):       return hash(self.amount)

m1 + m2                 # runs __add__
sorted([m2, m1])        # runs __lt__
print(m1)               # __str__     →  ₹500.00
m1                      # __repr__    →  Money(500.0)
```

**`__str__` vs `__repr__`** — the question:
> *"`__str__` is the friendly version for end users; `__repr__` is the unambiguous one for developers and debugging. If you only write one, write `__repr__` — `print()` falls back to it."*

**`__eq__` and `__hash__` travel together.** Define `__eq__` without `__hash__` and Python sets your object **unhashable** — it can no longer go in a set or be a dict key. Two equal objects must have equal hashes, or dicts break.

| Dunder | Triggered by | Give it when |
|---|---|---|
| `__init__` | `Thing()` | always |
| `__repr__` | debugging, `print` fallback | **always** — one line, saves hours |
| `__str__` | `str(x)`, `print` | users see it |
| `__eq__` + `__hash__` | `==`, sets, dict keys | comparing by value |
| `__len__` | `len(x)` | it's a collection |
| `__lt__` | `<`, `sorted()` | it has a natural order |

**Recall:** *`__str__` vs `__repr__` — which do you write if you only write one, and why?*

> ✍️ **Blank page, 4 min.** The dunder table from memory + the `__eq__`/`__hash__` rule.

---

## ② O-04 · Encapsulation — protecting a promise

**Anchor:** *"A class protects a promise, not a variable."*

The textbook answer — *"hide data with private variables, provide getters and setters"* — is **why so much OOP code is bloated.** It produces classes that are dicts with twenty extra lines.

**The real reason:**
```python
acc.balance = -50000      # nothing stopped this
acc.balance = "hello"     # or this
```
The promise *"a balance is a number, never below zero"* has no way to be kept — and when you find the corruption you have **no idea which line did it**.

```python
class BankAccount:
    def __init__(self, balance: float):
        if balance < 0: raise ValueError("negative balance")
        self._balance = balance

    def withdraw(self, amount: float) -> None:
        if amount > self._balance: raise ValueError("insufficient funds")
        self._balance -= amount
```
Now the promise is kept in **exactly two places** and there is no third way in.

**The test:**
> Is there a rule about this data that must always be true?
> Yes → internal, plus methods that respect it. No → **leave it public.** A `Point` with `x`,`y` has no rule; don't write `get_x()`.

| Written | Means | Enforced? |
|---|---|---|
| `balance` | public | — |
| `_balance` | "internal, don't touch" | **No.** Convention only. |
| `__balance` | mangled to `_Class__balance` | Accidents unlikely, not impossible |

**Python has no true private.** Say exactly that — reciting Java's rules is the giveaway that you memorised someone else's language.

**`@property` — looks like data, runs like a method:**
```python
class Circle:
    def __init__(self, r): self.radius = r
    @property
    def area(self):                       # computed on demand — never stale
        return 3.14159 * self.radius ** 2

>>> c.area          # no parentheses
```
**That's the Python argument against writing getters up front.** In Java you write them defensively because you can't change your mind later. In Python you *can* — so don't pay the cost until you need it.

**Gotcha:** inside `__init__`, `self.balance = x` **runs your setter**; `self._balance = x` skips it. Know which you're doing.

**Recall:** *What's the one question that decides whether a field should be private?*

## 🔨 Build it — 25 min

In `v1_classes.py`:
```python
# 1. Rename User.balances → self._balances.
#    Add @property balances returning a COPY: dict(self._balances)
#    Try  user.balances["ghost"] = 999  → confirm the real one is untouched.
# 2. Add @property net_balance and @property status
#    ("settled up" / "owes ₹X" / "is owed ₹X")
# 3. Give Expense: __str__ (human), __repr__ (dev), __eq__ (same id), __hash__.
#    Put two Expenses in a set — confirm dedupe works. Remove __hash__,
#    watch it break, read the error. Then put it back.
# 4. Make Expense.amount a property with a setter: 0 < amount <= 1_000_000.
#    Tiny test at the bottom: try 0, -5, 2_000_000, 500 → print PASS/FAIL.
```

**Acceptance:** four PASS lines, and you saw the unhashable error yourself.

## 🎤 Out loud — 6 min
1. **"What is encapsulation actually for?"** 2 min. If your answer contains "getters and setters", redo it. The word is **invariant**.
2. **"`__str__` vs `__repr__`?"** 60 sec.

## Ledger — 2 min
> Mark O-03, O-04. Tick S5.

---
---

# S6 · Composition, inheritance, MRO

## ⓪ Cold open — 8 min. Notes CLOSED.
1. The one test for whether a field should be private.
2. `__eq__` without `__hash__` — what breaks?
3. *(S4)* Class vs instance variable — the shared-list bug.

## ① O-05 · Composition

**Anchor:** *"A car HAS an engine. A car IS NOT an engine."*
**Yaad rakho:** *"Gaadi mein engine hai — gaadi engine nahi hai."*

```
COMPOSITION (has-a)                 INHERITANCE (is-a)
  ┌─────────┐                        ┌──────────┐
  │   Car   │                        │ Vehicle  │
  │ engine ─┼──→ ┌────────┐          └────┬─────┘
  └─────────┘    │ Engine │          ┌────▼─────┐
                 └────────┘          │   Car    │
  swap at runtime                    └──────────┘  fixed when you write it
```

**The test:** say *"A ___ IS A ___"* out loud. Sounds wrong → composition.

```python
class Car:
    def __init__(self, engine): self.engine = engine
    def start(self): self.engine.ignite()

Car(PetrolEngine());  Car(ElectricEngine())    # same class, different behaviour
```

**That is what "favour composition over inheritance" actually means** — a line you'll be asked to explain, and which almost nobody explains beyond quoting it. With inheritance you'd need `PetrolCar`, `ElectricCar`, then `ElectricSportsCar`, and the combinations explode.

**Recall:** *You need class A to use class B. What sentence do you say to decide how?*

---

## ② O-06 · Inheritance — and overriding vs overloading

**Anchor:** *"Inherit only when the child is a kind of the parent — and takes nothing away."*

```python
class Vehicle:
    def __init__(self, plate): self.plate = plate
    def spots_needed(self): raise NotImplementedError

class Car(Vehicle):
    def __init__(self, plate, doors=4):
        super().__init__(plate)         # ← FIRST LINE. Always.
        self.doors = doors
    def spots_needed(self): return 1    # override — the child's version wins
```

**`super().__init__()`** runs the parent's init on you. Forget it and `self.plate` never gets set — with the `AttributeError` landing far from the real cause.

### Overriding vs overloading — asked constantly, and Python has a twist

```
OVERRIDING   same name, same signature, in a SUBCLASS. Runtime.  ✅ Python has it.
OVERLOADING  same name, DIFFERENT signatures, same class.        ❌ Python does NOT.
```

```python
class A:
    def f(self, x): ...
    def f(self, x, y): ...     # this does NOT overload — it REPLACES the first
```

**The answer:** *"Python doesn't support method overloading — a second definition just replaces the first. You get the same effect with default arguments, `*args`, or `functools.singledispatch`."*

That's a **great** answer, because most candidates recite Java's version and get caught.

### The three smells — when inheritance is wrong

**1 · Overriding to disable**
```python
class Penguin(Bird):
    def fly(self): raise NotImplementedError    # 🚩
```
`Bird` promised flight; `Penguin` withdraws it. **A child may add, and may change *how*. It may never take away.**

**2 · Inheriting to reuse code.** `class Stack(list)` 🚩 — you also inherited `insert`, `sort`, indexing, none of which a stack should allow. Use composition: hold a `self._items`.

**3 · Deep trees.** Three levels and nobody can tell where a method comes from. **Two is plenty.**

**The two-part test:**
```
1. "B IS A kind of A" — sounds wrong → composition.
2. Can B do EVERYTHING A promises, with nothing disabled? No → composition.
```
Test 2 is **Liskov Substitution**, arriving early. You'll meet the acronym in S9 already owning the idea.

**Recall:** *Does Python support method overloading? What do you use instead?*

---

## ③ O-07 · MRO and the diamond problem

**Anchor:** *"Multiple parents, one search order — and Python publishes it."*

```
        A                A has method f()
       ╱ ╲               B and C both override it
      B   C              D inherits from both. Whose f() runs?
       ╲ ╱
        D               ← the "diamond problem"
```

```python
class A:
    def f(self): print("A")
class B(A):
    def f(self): print("B")
class C(A):
    def f(self): print("C")
class D(B, C): pass

D().f()              # "B"
D.__mro__            # (D, B, C, A, object)   ← left to right, then up
```

**Python resolves it with the MRO (Method Resolution Order)** — computed by the C3 linearisation, and you can always just *print* it. Left-to-right across the bases, then upward, and each class appears once.

**`super()` follows the MRO, not "the parent."** In a diamond, `super()` inside `B` can call `C` — which surprises everyone the first time.

**The answer:** *"Python allows multiple inheritance and resolves conflicts with the MRO — you can check it with `__mro__`. Java avoids the problem by only allowing multiple interfaces, not multiple classes."*

**Gotcha:** you don't need to compute C3 by hand. **You need to know the name, that `__mro__` exists, and that it goes left to right.** That's the whole expected answer at this level.

**Recall:** *`class D(B, C)` — which parent's method wins, and how do you check?*

> ✍️ **Blank page, 5 min.** Draw the diamond. Write the MRO order and the overriding-vs-overloading contrast.

## 🔨 Build it — 25 min

```python
# 1. Composition, 8 min:
#    class Service that takes a logger object in __init__ and calls self.logger.log()
#    Write ConsoleLogger and FileLogger. Make one Service log to console,
#    another to file — WITHOUT writing a second Service class.
#
# 2. Split hierarchy, 10 min:
#    Split (base, __init__(user), amount() → NotImplementedError)
#    EqualSplit / ExactSplit / PercentSplit — all calling super().__init__(user)
#    Build a mixed list, print each amount().
#
# 3. MRO, 7 min:
#    Write the A/B/C/D diamond above. Print D().f() and D.__mro__.
#    Then swap to class D(C, B) and print both again. Watch the answer change.
```

**Acceptance:** you saw the MRO change when you swapped the base order.

## 🎤 Out loud — 6 min
1. **"When should you NOT use inheritance?"** 2 min — Penguin and `Stack(list)`.
2. **"Does Python support method overloading?"** 60 sec.

## Ledger — 2 min
> Mark O-05, O-06, O-07. Tick S6.

---
---

# S7 · Polymorphism & abstraction

## ⓪ Cold open — 8 min. Notes CLOSED.
1. Does Python support method overloading? What do you use instead?
2. `class D(B, C)` — which method wins, and how do you check?
3. *(S5)* `__str__` vs `__repr__`. *(S6)* has-a vs is-a test.

## ① O-08 · Polymorphism & duck typing

**Anchor:** *"One loop, many types — the if-chain disappears."*

### The code you've been writing your whole life
```python
def calculate(split, total, n):
    if split.type == "equal":     return total / n
    elif split.type == "exact":   return split.value
    elif split.type == "percent": return total * split.percent / 100
    elif split.type == "shares":  ...          # ← EDIT this function. Again.
```
And there will be four more functions shaped exactly like it — `validate`, `display`, `serialise` — and you *will* forget to update one.

### The replacement
```python
for split in splits:
    print(split.amount())        # each object knows its own answer
```

```
       BEFORE                          AFTER
   ┌──────────────┐               ┌───────────────┐
   │ if equal:    │               │ split.amount()│
   │ elif exact:  │               └───────┬───────┘
   │ elif percent:│                ┌──────┼──────┐
   └──────────────┘                ▼      ▼      ▼
   caller decides                Equal  Exact  Percent
```

**The interview answer.** Most candidates say *"one interface, many forms"* — a memorised phrase that demonstrates nothing. Say this:
> *"It lets me replace a type-checking if-chain with a single call, so adding a new type means adding a class instead of editing existing code."*

**Compile-time vs runtime polymorphism** — if asked: *"Java has both — overloading is compile-time, overriding is runtime. Python only really has runtime, since it has no overloading and resolves everything dynamically."*

**Duck typing — Python needs no base class:**
```python
class Dog:      def speak(self): return "bhow"
class Doorbell: def speak(self): return "ding"      # unrelated to Dog

for t in [Dog(), Doorbell()]:
    print(t.speak())        # works
```
Python checks the **method exists**, at call time. *(You often still want a base class — that's next.)*

**Recall:** *What does polymorphism let you delete from your code?*

---

## ② O-09 · ABC as a contract

**Anchor:** *"An ABC is a promise Python enforces."*

Duck typing works — until it doesn't:
```python
class BrokenSplitter:
    def splitt(self, amount, users): ...   # typo. Nothing complains.

group = Group(BrokenSplitter())            # accepted happily
group.add_expense(...)                     # 💥 AttributeError, 200 lines later
```

```python
from abc import ABC, abstractmethod

class SplitStrategy(ABC):
    @abstractmethod
    def split(self, amount: float, users: list) -> dict[str, float]: ...

    def name(self) -> str:                 # concrete methods allowed too
        return self.__class__.__name__

>>> SplitStrategy()     # TypeError: Can't instantiate abstract class
>>> Broken()            # TypeError: ...with abstract method split
```

**The error now arrives at object creation** — right next to the mistake.

| | Duck typing | ABC |
|---|---|---|
| Error timing | at call, far away | **at creation, immediately** |
| Documents the contract | no | **yes — it's the file** |

**The honest limit:** an ABC checks the method *exists*, not that your implementation is sane. Contract about shape, not behaviour.

**"Does Python have interfaces?"**
> *"Not as a keyword. The equivalent is an abstract base class with `@abstractmethod` — or plain duck typing, since Python checks at call time. ABCs are what you use when you want the contract enforced and documented."*

**Abstract class vs interface** — the classic:
> *"An abstract class can have both abstract and concrete methods and holds state; an interface (in Java) is only a contract. In Python there's no separate keyword — an ABC with only abstract methods is your interface."*

**Recall:** *What does an ABC give you that duck typing doesn't?*

> ✍️ **Blank page, 4 min.** A full ABC with one abstract and one concrete method + a subclass, and the two errors it produces.

## 🔨 Build it — 30 min

```python
# 1. Delete the if-chain (8 min):
#    Write total_owed(splits) with an if/elif chain. Make it work.
#    Rewrite as: return sum(s.amount() for s in splits)
#    Add SharesSplit. Confirm version 2 works untouched and version 1 doesn't.
#    Write that gap in a comment.
#
# 2. SplitStrategy ABC (12 min):
#    @abstractmethod split(amount, users) -> dict
#    @abstractmethod validate(amount, users) -> bool
#    concrete name()
#    EqualSplit / ExactSplit(amounts) / PercentSplit(percents)
#      validate: Equal always True · Exact sums to total · Percent sums to 100
#
# 3. Rewrite Expense (10 min) to store a list of splits, with
#    validate() and apply() — BOTH free of any if-chain on split type.
#    Handle the float trap: ₹100 split 3 ways isn't exactly 100.
#    Pick tolerance OR give the remainder to the payer. One comment saying why.
```

**Acceptance:** grep your file for `split_type ==`. **Zero hits.** `SplitStrategy()` raises.

> The float thing is a real interview follow-up — *"how do you handle the paisa that doesn't divide?"* Having an answer puts you ahead of most freshers.

## 🎤 Out loud — 8 min
1. **"What is polymorphism, and what problem does it solve?"** 90 sec.
2. **"Does Python have interfaces?"** 60 sec.
3. **"Abstract class vs interface?"** 60 sec.

## Ledger — 2 min
> Mark O-08, O-09. Tick S7.
>
> **All four pillars done** — encapsulation (S5), inheritance (S6), polymorphism + abstraction (S7). Next: `p3-design.md`.
