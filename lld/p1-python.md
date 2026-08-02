# Part 1 · Python vocabulary — S1, S2, S3

**One session per sitting. ~70 min each. Stop at the horizontal rule.**

> Every question in this part gets asked directly in placement interviews. Not "useful background" — literally asked, in these words.

---
---

# S1 · Objects, copies and identity

## ① P-01 · Mutable vs immutable

**Anchor:** *"Immutable can't change — so Python reuses it, and that's where the trap comes from."*

```
IMMUTABLE   int · float · str · tuple · bool · frozenset
MUTABLE     list · dict · set · your own classes
```

```python
s = "hello"
s.upper()          # returns a NEW string — s is unchanged
l = [1, 2]
l.append(3)        # the SAME list, modified in place
```

**The trap that gets asked:**

```python
def add(item, lst=[]):        # the default list is created ONCE, at def time
    lst.append(item)
    return lst

add(1)    # [1]
add(2)    # [1, 2]   ← the SAME list. Every call. Forever.

def add(item, lst=None):                     # ✅
    lst = lst if lst is not None else []
```

**And its mirror:**
```python
grid = [[0] * 3] * 2          # ❌ two references to ONE row
grid[0][0] = 9                # → [[9,0,0], [9,0,0]]
grid = [[0] * 3 for _ in range(2)]           # ✅
```

**Recall:** *Why does a mutable default argument keep its old value between calls?*

---

## ② P-02 · What `=` actually copies

**Anchor:** *"`=` copies the label, not the box."*

```
a = [1, 2, 3]
b = a                      a ──┐
                               ├──► [1, 2, 3]     one list, two names
b.append(4)                b ──┘
print(a)   # [1,2,3,4]  ← a changed too
```

```python
import copy
b = a.copy()            # SHALLOW — new outer list, same inner objects
b = copy.deepcopy(a)    # DEEP — copied all the way down

nested  = [[1, 2], [3, 4]]
shallow = nested.copy()
shallow[0].append(99)   # → nested is [[1,2,99],[3,4]] too. Inner list is shared.
```

**`is` vs `==`** — asked constantly:
```python
a = [1,2];  b = [1,2]
a == b     # True   — same VALUE
a is b     # False  — different OBJECTS
```

**The rule: `==` for values, `is` only for `None`.** Write `if x is None`, never `if x == None`.

**Recall:** *Shallow vs deep copy — what does shallow actually share?*

> ✍️ **Blank page, 4 min.** Draw two-labels-one-box. Write the `is`/`==` rule and the default-arg fix.

---

## ③ P-03 · Choosing the container

**Anchor:** *"Ordered? Unique? Keyed? — that's the whole decision."*

| | Ordered | Mutable | Duplicates | Lookup | Use when |
|---|---|---|---|---|---|
| `list` | ✅ | ✅ | ✅ | O(n) | a sequence you'll change |
| `tuple` | ✅ | ❌ | ✅ | O(n) | fixed record; **can be a dict key** |
| `set` | ❌ | ✅ | ❌ | **O(1)** | membership, dedupe |
| `dict` | ✅ (3.7+) | ✅ | keys unique | **O(1)** | lookup by key |

**Why a tuple can be a dict key and a list can't:** keys must be **hashable**, and hashable means immutable. A list could change after insertion and its hash would be wrong.

```python
d[(1, 2)] = "ok"      # ✅
d[[1, 2]] = "boom"    # TypeError: unhashable type: 'list'
```

**Recall:** *Why can a tuple be a dict key but a list can't?*

## 🔨 Build it — 20 min

Create `splitwise/warmup.py`. Everything must **run**.

```python
# 1. Write the buggy add(item, lst=[]) and CALL IT THREE TIMES, printing each.
#    Watch it accumulate. Then fix it.
# 2. nested = [[1,2],[3,4]]. Shallow-copy, mutate the inner list, print both.
#    Repeat with deepcopy. Print both again.
# 3. Try d[[1,2]] = "x" inside try/except. Print the exact error.
# 4. Write is_anagram(a, b) with a Counter, and dedupe(items) with a set.
```

**Acceptance:** you personally watched the default-arg bug accumulate, and can quote the `unhashable type` error.

## 🎤 Out loud — 5 min
1. **"Difference between a list and a tuple?"** 60 sec. End on hashability.
2. **"`is` vs `==`?"** 45 sec.

## Ledger — 2 min
> Mark P-01, P-02, P-03. Tick S1.

---
---

# S2 · Functions & failure

## ⓪ Cold open — 8 min. Notes CLOSED.
1. Why does a mutable default argument keep its old value?
2. Shallow vs deep copy — what does shallow share?
3. Why can a tuple be a dict key but a list can't?

> Mark ✅/⚠️/❌. ❌ → 🔴 in `ledger.md`.

## ① P-04 · The idioms interviewers expect

**Anchor:** *"`*args` collects positionals, `**kwargs` collects keywords."*

```python
def f(*args, **kwargs):
    print(args)      # a TUPLE of positional arguments
    print(kwargs)    # a DICT of keyword arguments

f(1, 2, name="d")    # (1, 2)  ·  {'name': 'd'}
```

**Unpacking is the same syntax in reverse:**
```python
print(*[1, 2, 3])            # print(1, 2, 3)
setup(**{"a": 1, "b": 2})    # setup(a=1, b=2)
```

**Comprehensions** — you know these from DSA:
```python
[x*2 for x in nums if x > 0]     # list
{k: v for k, v in pairs}         # dict
{x for x in nums}                # set
(x*2 for x in nums)              # GENERATOR — nothing built. See S3.
```

**`sorted` with a key — shows up everywhere:**
```python
sorted(users, key=lambda u: u.name)
sorted(items, key=lambda i: (i.dept, -i.salary))    # dept asc, salary desc
```

**lambda:** a one-expression anonymous function. Use it as a `key`. Don't use it for anything with a body — `def` is clearer and interviewers prefer it.

**Recall:** *`*args` collects into what type? `**kwargs`?*

---

## ② P-05 · Exceptions

**Anchor:** *"Ask forgiveness, not permission — and raise something with a name."*

```python
class InsufficientBalanceError(Exception):
    pass

raise InsufficientBalanceError(f"need ₹{amount}, have ₹{self.balance}")
```

**A named exception class reads far better than `raise Exception("...")`** — and interviewers notice immediately.

```python
try:
    risky()
except ValueError as e:      # specific first
    ...
except Exception as e:       # broad last
    ...
else:                        # ran only if NO exception
    ...
finally:                     # ALWAYS runs — cleanup goes here
    ...
```

**The Python style point (EAFP):**
```python
if key in d: v = d[key]        # LBYL — "look before you leap"  (the Java instinct)
try: v = d[key]                # EAFP — "ask forgiveness"        ← Python prefers this
except KeyError: v = None
```

**Gotcha:** a bare `except:` also catches `KeyboardInterrupt` — it swallows Ctrl-C. Always catch something specific.

**Recall:** *When does `finally` run? When does `else` run?*

> ✍️ **Blank page, 4 min.** The full try/except/else/finally skeleton and a custom exception class, from memory.

## 🔨 Build it — 20 min

```python
# In warmup.py:
# 1. summarise(*names, **options) that prints both. Call it three different ways.
# 2. users = [("d",22,90), ("p",22,80), ("r",21,95)]
#    Sort by age ascending, then score DESCENDING — in ONE sorted() call.
# 3. class InsufficientFundsError(Exception). withdraw(balance, amount) raises it.
#    Call it in try/except/else/finally with a print in EACH block,
#    so you can SEE the order they fire in.
```

**Acceptance:** you can state, from your own output, exactly when `else` and `finally` run.

## 🎤 Out loud — 5 min
> **"What are `*args` and `**kwargs`?"** 60 sec, including the reverse-unpacking use.

## Ledger — 2 min
> Mark P-04, P-05. Tick S2.

---
---

# S3 · Generators, decorators, and the GIL

> **The three highest-frequency "do you actually know Python" questions.** When an interviewer wants to separate you from someone who only did DSA, they ask these.

## ⓪ Cold open — 8 min. Notes CLOSED.
1. `*args` collects into what type? `**kwargs`?
2. When does `finally` run? When does `else` run?
3. *(S1)* `is` vs `==` — the rule.

## ① P-06 · Generators & `yield`

**Anchor:** *"`return` ends it. `yield` pauses it."*

```python
def squares(n):
    result = []
    for i in range(n):
        result.append(i*i)      # builds ALL of it in memory
    return result

def squares(n):
    for i in range(n):
        yield i*i               # produces ONE, pauses, resumes on next()
```

```
list version:   [0,1,4,...,999999]   ← a million items in RAM
generator:      one value at a time  ← constant memory
```

**What actually happens:**
```python
g = squares(3)     # NOTHING has run. You get a generator object.
next(g)            # runs to the first yield → 0, then FREEZES
next(g)            # thaws, continues → 1
next(g)            # → 4
next(g)            # StopIteration
```

**Where you'd use it:** a huge file line by line, streaming DB rows, infinite sequences — anything where the full list would blow memory.

**Iterable vs iterator** — the follow-up:
```
ITERABLE   has __iter__     (list, str, dict)   — can be looped over
ITERATOR   has __next__     (generator)         — produces values, remembers position

a list is iterable but NOT an iterator. iter(mylist) gives you the iterator.
```

**Gotcha:** a generator is **exhausted after one pass.** Loop it twice and the second loop sees nothing. Lists don't behave that way, and this bites everyone once.

**Recall:** *What's the difference between `return` and `yield`?*

---

## ② P-07 · Decorators

**Anchor:** *"A decorator is a function that wraps another function."*

You've already used three: `@property`, `@staticmethod`, `@dataclass`.

```python
import functools

def logged(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):        # ← accepts anything
        print(f"calling {func.__name__}")
        result = func(*args, **kwargs)
        print("done")
        return result
    return wrapper

@logged
def add(a, b):
    return a + b
```

```
@logged  is EXACTLY the same as:   add = logged(add)
                                         │
                                         └─ takes the original, returns a NEW
                                            function that calls it inside
```

**That one line is the whole concept.** The `@` is sugar for rebinding the name to the wrapped version.

**Real uses:** timing, logging, auth checks, caching (`@functools.cache` — the same thing you use for DP memoization).

**Gotcha:** without `@functools.wraps`, the wrapper replaces the function's `__name__` and docstring. Mentioning that unprompted is a strong signal.

**Recall:** *`@logged` above a function — what single line is it equivalent to?*

> ✍️ **Blank page, 5 min.** Write a decorator from memory, plus the one-line equivalent of `@`.

---

## ③ P-08 · The GIL, and `with`

**Anchor:** *"One Python thread runs at a time — so threads help with waiting, not with computing."*

```
GIL = Global Interpreter Lock. One thread executes Python bytecode at any instant.

CPU-BOUND (maths, loops)   → threads DON'T help. Use multiprocessing.
I/O-BOUND (network, disk)  → threads DO help — the GIL is released while waiting.
```

**The interview answer:** *"Because of the GIL, Python threads don't give true parallelism for CPU-bound work — you'd use multiprocessing for that. They still help for I/O-bound work, since the GIL is released while a thread waits."*

**`with` — anchor:** *"Opens it, and closes it even if you crash."*
```python
with open("f.txt") as f:     # __enter__ runs
    data = f.read()
                             # __exit__ runs — even if an exception was raised
```
Any object with `__enter__` and `__exit__` works. Files, locks, DB connections — anything that must be released.

**Recall:** *Does the GIL make threads useless? When do they still help?*

## 🔨 Build it — 20 min

```python
# 1. countdown(n) as a generator. Call next() four times on countdown(3),
#    printing each — including catching StopIteration.
# 2. Loop over the SAME generator twice. Print both loops. Explain the second.
# 3. Write a @timer decorator (time.perf_counter before and after).
#    Put it on a function summing 1..1_000_000. Print the elapsed time.
# 4. Print func.__name__ with and without @functools.wraps.
```

**Acceptance:** the empty second loop surprised you, and you can say why.

## 🎤 Out loud — 8 min
1. **"What is a generator and when would you use one?"** 90 sec.
2. **"What is a decorator?"** 90 sec. Use `add = logged(add)`.
3. **"What is the GIL?"** 60 sec. Include CPU-bound vs I/O-bound.

## Ledger — 2 min
> Mark P-06, P-07, P-08. Tick S3.
>
> **Python vocabulary done — 8 concepts.** Next: `p2-oop.md`, where you start writing classes.
