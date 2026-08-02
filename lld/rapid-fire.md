# Rapid Fire — your only revision file

**After a part is done you never reopen its lesson file.** This replaces all four. Syntax lookup while coding is fine — that's what the bottom is for.

---

## The 23 anchors

Cover the right column. Say each out loud. 5 minutes.

| Anchor | → |
|---|---|
| "Immutable can't change — so Python reuses it, and that's where the trap comes from." | P-01 Mutable vs immutable |
| "`=` copies the label, not the box." | P-02 Copies & identity |
| "Ordered? Unique? Keyed? — that's the whole decision." | P-03 Containers |
| "`*args` collects positionals, `**kwargs` collects keywords." | P-04 Idioms |
| "Ask forgiveness, not permission — and raise something with a name." | P-05 Exceptions |
| "`return` ends it. `yield` pauses it." | P-06 Generators |
| "A decorator is a function that wraps another function." | P-07 Decorators |
| "One Python thread runs at a time — threads help with waiting, not computing." | P-08 GIL · `with` |
| "`self` is whoever the method was called on." | O-01 `self` · class vars |
| "`@dataclass` writes the boring code; `Enum` stops the typos." | O-02 dataclass · method types |
| "Define the dunder and Python's own syntax starts working on your class." | O-03 Dunders |
| "A class protects a promise, not a variable." | O-04 Encapsulation |
| "A car HAS an engine. A car IS NOT an engine." | O-05 Composition |
| "Inherit only when the child is a kind of the parent — and takes nothing away." | O-06 Inheritance |
| "Multiple parents, one search order — and Python publishes it." | O-07 MRO |
| "One loop, many types — the if-chain disappears." | O-08 Polymorphism |
| "An ABC is a promise Python enforces." | O-09 ABC |
| "Can't describe the class without saying 'and'? It's two classes." | D-01 SRP |
| "Add a file, don't edit a file." | D-02 OCP |
| "Depend on the promise, not on the class that keeps it." | D-03 LSP · ISP · DIP |
| "`if type == ...` is a Strategy waiting to happen." | D-04 Strategy |
| "One place that knows how to build things." | D-05 Factory |
| "Don't call me — subscribe, and I'll call you." | D-06 Observer |
| "Clarify → nouns → verbs → relationships → code → extend." | L-01 The 6-step method |

---

## 40 questions, 1-line answers

### Python
| Q | A |
|---|---|
| Name three immutable and three mutable types. | int, str, tuple · list, dict, set. |
| Why does a mutable default argument keep its value? | Created **once** at def time — same object every call. |
| Fix for it? | `def f(x, lst=None)` then `lst = lst or []`. |
| `[[0]*3]*2` — what's wrong? | Two references to one row. Use a comprehension. |
| Shallow vs deep copy? | Shallow shares inner objects; deep copies all the way down. |
| `is` vs `==`? | Identity vs value. Use `is` **only** for `None`. |
| Why can a tuple be a dict key but a list can't? | Keys must be hashable = immutable. |
| `*args` / `**kwargs`? | Tuple of positionals / dict of keywords. |
| `print(*nums)` — what's that? | Unpacking — the same syntax in reverse. |
| Multi-key sort? | `sorted(x, key=lambda i: (i.a, -i.b))`. |
| When does `finally` run? `else`? | Always / only if no exception was raised. |
| Why not bare `except:`? | It swallows `KeyboardInterrupt` too. Catch something specific. |
| EAFP vs LBYL? | Try and catch vs check first. Python prefers EAFP. |
| `return` vs `yield`? | Ends the function vs pauses it, resuming on `next()`. |
| When would you use a generator? | Huge files, streamed rows, infinite sequences — constant memory. |
| Iterable vs iterator? | `__iter__` (can be looped) vs `__next__` (produces, remembers position). |
| Generator gotcha? | **Exhausted after one pass.** A second loop sees nothing. |
| What is a decorator? | A function that wraps another. `@logged` ≡ `add = logged(add)`. |
| Why `functools.wraps`? | Preserves the wrapped function's `__name__` and docstring. |
| What is the GIL? | One thread executes Python bytecode at a time. |
| Do threads ever help then? | Yes — I/O-bound work. The GIL is released while waiting. |
| CPU-bound work? | Use `multiprocessing`. |
| What does `with` guarantee? | `__exit__` runs even if an exception is raised. |

### OOP
| Q | A |
|---|---|
| Explain `self`. | The object left of the dot. `d.greet()` runs `User.greet(d)`. |
| Is `self` a keyword? | No — a convention. Any name works. |
| Why does `__init__` return nothing? | Python already created the object; init only fills it in. |
| Class vs instance variable? | Shared by all vs one per object. A mutable class var is shared — classic bug. |
| instance vs class vs static method? | `self` / `cls` / nothing. `classmethod` = alternative constructor. |
| What does `@dataclass` write? | `__init__`, `__repr__`, `__eq__`. |
| `__str__` vs `__repr__`? | Friendly vs unambiguous. Write `__repr__` if only one. |
| `__eq__` without `__hash__`? | Object becomes unhashable — no sets, no dict keys. |
| Operator overloading? | Define `__add__`, `__lt__` etc. — your class plugs into Python's syntax. |
| What is encapsulation for? | Protecting an **invariant** — not writing getters and setters. |
| Does Python have true private? | No. `_x` is convention, `__x` is name mangling. |
| Why `@property` over getters? | You can upgrade an attribute to computed later without breaking callers. |
| has-a vs is-a test? | Say "A ___ IS A ___." Sounds wrong → composition. |
| Why favour composition? | Swap the object at runtime; inheritance is fixed when you write it. |
| What does `super().__init__()` do? | Runs the parent's init on you. Without it, parent attributes never get set. |
| Overriding vs overloading? | Same signature in a subclass vs different signatures — **Python has no overloading.** |
| Then how do you fake it? | Default args, `*args`, or `functools.singledispatch`. |
| Three inheritance smells? | Overriding to disable · inheriting to reuse code · trees deeper than two. |
| Square/Rectangle problem? | Square couples width and height, breaking Rectangle's promise. LSP. |
| `class D(B, C)` — which wins? | B. Check `D.__mro__` — left to right, then up. |
| What is the diamond problem? | Two parents override the same method; MRO decides. Java avoids it via interfaces. |
| What does polymorphism let you delete? | A type-checking if-chain. |
| Compile-time polymorphism in Python? | Effectively none — no overloading, everything resolves at runtime. |
| Duck typing? | If the method exists, Python doesn't care about the class. |
| ABC vs duck typing? | ABC fails at **creation**, next to the mistake, and documents the contract. |
| Does Python have interfaces? | No keyword — an ABC with only abstract methods is the equivalent. |
| Abstract class vs interface? | Abstract class can hold state and concrete methods; an interface is pure contract. |

### Design
| Q | A |
|---|---|
| SRP test? | Describe the class in one sentence. Any "and" is a second class. |
| SRP over-correction? | One coherent responsibility, not one method. |
| OCP in one line? | Add a file, don't edit a file. |
| When NOT to apply OCP? | When there realistically won't be a version 2. |
| LSP test? | Swap the child in for the parent — does anything break? |
| ISP smell? | A subclass implementing a method with `pass` or `NotImplementedError`. |
| DIP fix? | Take the dependency as a parameter instead of creating it inside. |
| Why does DI matter? | Testability. Say "I'd inject it so it's testable." |
| Strategy trigger? | `if type == ...` choosing between **behaviours**. |
| Strategy vs Factory? | *How* something is done vs *which object* is created. |
| Observer trigger? | "When X happens, tell A, B and C." |
| Singleton — honest answer? | Global state, untestable, hides dependencies. Use it, but inject it. |
| The 6 steps? | Clarify → nouns → verbs → relate → code → extend. |
| Biggest fresher mistake in a design round? | **Over-engineering.** Patterns nothing needed. |

---

## The chooser — when you're staring at a blank page

| Situation | Reach for |
|---|---|
| Two variables always change together | Make them a class |
| A class needs another class's data | **Composition** |
| B is a *kind of* A, removes nothing | **Inheritance** |
| `if type == "x": … elif "y": …` | **Strategy** |
| Creation logic scattered across files | **Factory** |
| "When X happens, tell A, B and C" | **Observer** |
| A class description needs "and" | **Split it** (SRP) |
| A new feature means editing a class | **Rethink** (OCP) |

---

## Python syntax — look this up freely, no shame

```python
from dataclasses import dataclass, field
from abc import ABC, abstractmethod
from enum import Enum
import functools, copy

@dataclass
class Expense:
    amount: float
    tags: list[str] = field(default_factory=list)      # NEVER = []

@dataclass(frozen=True)                    # immutable
class Money: amount: float

class SplitType(Enum): EQUAL = "equal"
SplitType.EQUAL.value                      # 'equal'

class Strategy(ABC):
    @abstractmethod
    def run(self) -> None: ...

class Child(Parent):
    def __init__(self, x):
        super().__init__(x)                # ALWAYS first
        self.y = 1

class User:
    count = 0                              # class variable
    def __init__(self, n):
        self._n = n
        User.count += 1
    def __repr__(self):  return f"User({self._n})"
    def __str__(self):   return self._n
    def __eq__(self, o): return isinstance(o, User) and self._n == o._n
    def __hash__(self):  return hash(self._n)
    def __lt__(self, o): return self._n < o._n
    @property
    def n(self): return self._n
    @n.setter
    def n(self, v):
        if not v: raise ValueError("empty")
        self._n = v
    @staticmethod
    def valid(e): return "@" in e
    @classmethod
    def from_str(cls, s): return cls(*s.split(","))

def logged(func):                          # decorator
    @functools.wraps(func)
    def wrapper(*a, **kw):
        return func(*a, **kw)
    return wrapper

def gen(n):                                # generator
    for i in range(n): yield i

class OutOfStockError(Exception): pass

b = copy.deepcopy(a)
sorted(x, key=lambda i: (i.a, -i.b))
with open("f") as f: ...
```

**Traps:**
```python
def f(x, lst=[]):        # ❌ same list every call     → lst=None, then lst = lst or []
items: list = []         # ❌ in a dataclass           → field(default_factory=list)
grid = [[0]*3]*2         # ❌ shared rows              → [[0]*3 for _ in range(2)]
class Cart: items = []   # ❌ shared by every instance → set self.items in __init__
def __eq__ without __hash__      # ❌ object becomes unhashable
class C(P): def __init__(s): ...  # ❌ forgot super().__init__()
```

---

## If you have 5 minutes before an interview

Read the **23 anchors** out loud, then say the **6 steps** once.
