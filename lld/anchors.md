# Anchors — all of OOP + LLD on one page

**How to use:** cover the right column. Read the anchor aloud, reconstruct the concept, then check. Five minutes, once a week — and the morning of any interview.

---

| Anchor (say it out loud) | → Concept |
|---|---|
| "In Python, everything is an object — even a function, even a class" | O-01 Everything is an object |
| "`@dataclass` writes the boring code; `Enum` stops the typos" | O-02 dataclass · Enum · hints |
| "Nouns become classes, verbs become methods" | O-03 Nouns → classes |
| "If two variables always travel together, they're one object" | O-04 Data that travels together |
| "`self` is whoever the method was called on" | O-05 `self` |
| "`__init__` builds it, `__repr__` shows it to you" | O-06 `__init__` and `__repr__` |
| "A class protects a promise, not a variable" | O-07 Invariants |
| "`@property` — looks like data, runs like a method" | O-08 `@property` |
| "A car HAS an engine. A car IS NOT an engine." | O-09 Composition |
| "Only inherit when the child is genuinely a *kind of* the parent" | O-10 Inheritance |
| "If you're overriding to *remove* behaviour, it was never is-a" | O-11 When inheritance is wrong |
| "One loop, many types — the if-chain disappears" | O-12 One loop, many types |
| "If it has the method, Python doesn't care what class it is" | O-13 Duck typing |
| "An ABC is a promise the compiler enforces" | O-14 ABC as a contract |
| "Can't describe the class without saying 'and'? It's two classes." | O-15 SRP |
| "Add a file, don't edit a file" | O-16 OCP |
| "Depend on the promise, not on the class that keeps it" | O-17 LSP · ISP · DIP |
| "`if type == ...` is a Strategy waiting to happen" | O-18 Strategy |
| "One place that knows how to build things" | O-19 Factory |
| "Don't call me — subscribe, and I'll call you" | O-20 Observer |
| "Clarify → nouns → verbs → relationships → code → extend" | O-21 The 6-step method |

---

## The 5 Hinglish hooks

For these, the Hindi version *is* the better thought. Either one counts as correct recall.

| Yaad rakho | → Concept |
|---|---|
| *"`self` matlab — jis object pe method call hua, wahi."* | O-05 `self` |
| *"Bahar se button, andar se machine."* | O-07/O-08 Encapsulation |
| *"Gaadi mein engine hai — gaadi engine nahi hai."* | O-09 Composition vs inheritance |
| *"Naam ek, kaam alag."* | O-12 Polymorphism |
| *"Kaam wahi, tareeka alag."* | O-18 Strategy |

---

## The chooser — when you're staring at a blank page

| The situation | Reach for |
|---|---|
| Two variables always change together | Make them a class |
| A class needs another class's data to do its job | **Composition** — give it the object |
| B is genuinely a *kind of* A, with no removed behaviour | **Inheritance** |
| `if type == "x": ... elif type == "y": ...` | **Strategy** |
| Object creation has messy `if`s scattered around | **Factory** |
| "When X happens, tell A, B and C" | **Observer** |
| A class description needs the word "and" | **Split it** (SRP) |
| A new feature means editing an existing class | **Rethink** (OCP) |

---

## The LLD interview script (memorise this shape)

```
1. CLARIFY   3 questions. Scope, scale, edge cases.       (3 min)
2. NOUNS     List entities from the requirements.          (3 min)
3. VERBS     What can each one do? → methods.              (3 min)
4. RELATE    has-a? is-a? Draw the boxes.                  (5 min)
5. CODE      Core flow first. Working > complete.         (25 min)
6. EXTEND    "What if we needed X?" Answer before asked.   (5 min)
```

**The trap:** starting at step 5. Steps 1–4 are what's actually being scored.
