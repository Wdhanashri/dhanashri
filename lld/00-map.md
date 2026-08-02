# The Map — 14 sessions, one project, one interview skill

```
   PART 1              PART 2                PART 3           PART 4
   Python           Why classes,          Clean it up      Design it
   toolkit          and the 4 pillars     (SOLID +          for real
                                           patterns)
   ┌────┐           ┌──────────────┐      ┌─────────┐     ┌──────────┐
   │ L1 │  ────→    │ L2 · L3 · L4 │ ───→ │ L9  L10 │ ──→ │ L13 · L14│
   └────┘           │ L5 · L6 · L7 │      │ L11 L12 │     │  capstone│
                    │      L8      │      └─────────┘     └──────────┘
                    └──────────────┘

   the same Splitwise codebase, getting better in every single one
   ─────────────────────────────────────────────────────────────────→
   ugly dict          real classes          clean design      whiteboard-ready
```

---

## The 14 sessions

| # | Session | You'll be able to | Code you write |
|---|---|---|---|
| **L1** | Python for OOP | Use `@dataclass`, `Enum`, type hints, `__repr__` | Warm-ups |
| **L2** | Why classes exist at all | Look at a mess and see the objects hiding in it | Splitwise v0 (deliberately ugly) |
| **L3** | `self` and `__init__`, properly | Stop being confused by `self`. Permanently. | Splitwise v1 — real classes |
| **L4** | Encapsulation | Protect an invariant, use `@property` | Balances that can't go wrong |
| **L5** | Composition | Choose has-a over is-a by default | `Group` holds `User`s |
| **L6** | Inheritance — and when *not* to | Apply the is-a test, use `super()` | `Split` hierarchy |
| **L7** | Polymorphism | Delete an if-chain with one loop | Kill the `if split_type ==` |
| **L8** | Abstraction | Write an ABC that forces a contract | `SplitStrategy` |
| **L9** | SOLID — SRP & OCP | Spot a class doing too much, in 5 seconds | Big refactor |
| **L10** | SOLID — LSP, ISP, DIP | Depend on promises, not on classes | Injection |
| **L11** | Strategy & Factory | Recognise the two patterns you'll actually use | **Splitwise, final** |
| **L12** | Observer (+ Singleton, carefully) | Wire up notifications without coupling | Notification system |
| **L13** | The LLD method · Parking Lot | Run a 45-min design interview, step by step | Parking Lot, guided |
| **L14** | Solo machine coding · **Gate** | Do it alone, timed, cold | Vending Machine |

---

## The 21 concepts

| Part | Concepts |
|---|---|
| Python | O-01 Everything is an object · O-02 dataclass, Enum, type hints |
| Why classes | O-03 Nouns→classes, verbs→methods · O-04 Data that travels together |
| Objects | O-05 `self` · O-06 `__init__` and `__repr__` |
| Encapsulation | O-07 Invariants · O-08 `@property` |
| Relationships | O-09 Composition (has-a) · O-10 Inheritance (is-a) · O-11 When inheritance is wrong |
| Polymorphism | O-12 One loop, many types · O-13 Duck typing |
| Abstraction | O-14 ABC as a contract |
| SOLID | O-15 SRP · O-16 OCP · O-17 LSP+ISP+DIP |
| Patterns | O-18 Strategy · O-19 Factory · O-20 Observer |
| LLD | O-21 The 6-step method |

Every one has an anchor in `anchors.md` and a scheduled recall in `ledger.md`.

---

## What "done" looks like

At the end of L14 you should be able to, cold, in 45 minutes:

- [ ] Ask 3 clarifying questions before writing anything
- [ ] Turn a problem statement into 4–6 classes with sensible responsibilities
- [ ] Write working Python for the core flow
- [ ] Use **one** pattern, and justify it in a sentence
- [ ] Say what you'd change if a requirement were added

That's the bar for a fresher LLD round. Not more. **Over-engineering is the most common way freshers fail this round** — interviewers notice when you bolt on a Factory that nothing needed.

---

## The honest scope

This course does **not** make you a design expert. It makes you someone who can walk into an SDE LLD round, produce a clean small design, and defend it.

That is exactly, and only, what a final-year student is asked to do.
