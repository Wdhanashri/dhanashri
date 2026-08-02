# Cheatsheet — Python OOP syntax

**Open this while coding. That's what it's for.** Looking up syntax is not cheating; forgetting the *idea* is the problem, and this page has no ideas in it.

---

## A class, all the pieces

```python
from dataclasses import dataclass, field
from abc import ABC, abstractmethod
from enum import Enum
from typing import Optional

class User:
    company = "Splitwise"                    # class attribute — shared by all

    def __init__(self, name: str, email: str):
        self.name = name                     # instance attributes
        self.email = email
        self._balance = 0.0                  # _ = "internal, please don't touch"

    def __repr__(self) -> str:               # what you see when you print it
        return f"User({self.name}, ₹{self._balance})"

    def __eq__(self, other) -> bool:
        return isinstance(other, User) and self.email == other.email

    @property                                # looks like data, runs like a method
    def balance(self) -> float:
        return self._balance

    @balance.setter
    def balance(self, value: float) -> None:
        if value < -100_000:
            raise ValueError("balance too low")
        self._balance = value

    def pay(self, amount: float) -> None:    # instance method — needs self
        self._balance -= amount

    @staticmethod
    def is_valid_email(email: str) -> bool:  # no self — just lives here for tidiness
        return "@" in email

    @classmethod
    def from_string(cls, s: str) -> "User":  # alternative constructor
        name, email = s.split(",")
        return cls(name, email)
```

---

## dataclass — skips the boilerplate

```python
@dataclass
class Expense:
    amount: float
    paid_by: str
    description: str = ""                    # default
    tags: list[str] = field(default_factory=list)   # NEVER `= []`

# gives you __init__, __repr__, __eq__ for free
e = Expense(500, "dhanashri", "dinner")
```

```python
@dataclass(frozen=True)     # immutable — can't be changed after creation
class Money:
    amount: float
    currency: str
```

---

## Enum — kills magic strings

```python
class SplitType(Enum):
    EQUAL = "equal"
    EXACT = "exact"
    PERCENT = "percent"

SplitType.EQUAL           # <SplitType.EQUAL: 'equal'>
SplitType.EQUAL.value     # 'equal'
SplitType("equal")        # look up by value

# typo "eqaul" → crashes immediately, instead of silently doing nothing
```

---

## Inheritance

```python
class Vehicle:
    def __init__(self, plate: str):
        self.plate = plate

    def size(self) -> int:
        raise NotImplementedError

class Car(Vehicle):
    def __init__(self, plate: str, doors: int):
        super().__init__(plate)              # ALWAYS call this first
        self.doors = doors

    def size(self) -> int:                   # override
        return 2

isinstance(my_car, Vehicle)   # True
```

---

## Abstract base class — an enforced contract

```python
class SplitStrategy(ABC):
    @abstractmethod
    def split(self, amount: float, people: list[str]) -> dict[str, float]:
        ...                                  # no body needed

class EqualSplit(SplitStrategy):
    def split(self, amount, people):
        share = amount / len(people)
        return {p: share for p in people}

SplitStrategy()      # TypeError — can't instantiate an abstract class
EqualSplit()         # fine
```

If a subclass forgets `split`, Python refuses to create it. **That's the point.**

---

## Access levels (Python is honest about this)

| Written | Means | Enforced? |
|---|---|---|
| `name` | public | — |
| `_name` | "internal, don't touch" | **No** — convention only |
| `__name` | name-mangled to `_ClassName__name` | Sort of — makes accidents unlikely |

Python has **no true private**. If an interviewer asks, say exactly that — it's the correct answer, and reciting Java's rules is the giveaway that you memorised someone else's language.

---

## Useful dunders

| Dunder | Triggered by | Give it when |
|---|---|---|
| `__init__` | `Thing()` | always |
| `__repr__` | `print(x)`, debugging | always — it makes debugging survivable |
| `__str__` | `str(x)` | only if users see it |
| `__eq__` | `a == b` | comparing by value |
| `__hash__` | dict keys, sets | whenever you define `__eq__` |
| `__len__` | `len(x)` | it's a collection |
| `__lt__` | `<`, `sorted()` | it has a natural order |

---

## Exceptions

```python
class InsufficientBalanceError(Exception):
    pass

if amount > self.balance:
    raise InsufficientBalanceError(f"need ₹{amount}, have ₹{self.balance}")

try:
    user.pay(1000)
except InsufficientBalanceError as e:
    print(f"failed: {e}")
```

Custom exception classes read far better than `raise Exception("...")` — and interviewers notice.

---

## Traps that will bite you

```python
def add(item, lst=[]):        # ❌ the SAME list every call, forever
def add(item, lst=None):      # ✅
    lst = lst or []

@dataclass
class Bad:
    items: list = []                              # ❌ TypeError
    items: list = field(default_factory=list)     # ✅

self.balance = balance        # ❌ inside __init__ when you have a @property setter
self._balance = balance       # ✅  (or let the setter run — but know which)

class Child(Parent):
    def __init__(self, x):
        self.x = x            # ❌ forgot super().__init__() — parent attrs missing
```
