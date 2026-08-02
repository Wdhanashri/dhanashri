# SDE Interview Prep — Fresh Graduate, India

> The complete map of what actually gets asked. Not everything that exists — everything that **matters**.

**Built for one learner, one goal:** crack an SDE role as a final-year CS student, using a method where nothing covered gets forgotten.

---

## The 80/20 up front

If you only had 100 hours, you'd spend them like this:

| Area | Weight | Why |
|---|---|---|
| **DSA + problem solving** (Python · NeetCode 150) | **50%** | Every single company screens on this. Nothing else compensates for failing here. |
| **CS fundamentals** (OS · DBMS · CN · OOP) | **20%** | Round 2 at product companies, round 1 at service companies. Cheap marks. |
| **LLD / OOP design** | **10%** | Now standard for freshers at product companies. Most candidates skip it — easy edge. |
| **Projects + resume** | **10%** | Every interview opens here. A weak answer about your own project is unrecoverable. |
| **Aptitude + OA format** | **5%** | Pure gatekeeping for mass recruiters. Ignore it and you never reach a human. |
| **HLD basics + behavioural** | **5%** | Awareness-level only for freshers. Don't over-invest. |

**The one non-negotiable:** you cannot substitute effort in the other 50% for weakness in DSA.

---

## 1 · DSA — NeetCode 150 is the syllabus

**Language: Python.** **Scope: NeetCode 150. Nothing beyond it.**

Interviews don't test problems, they test **pattern recognition**. NC150 is the right target because it's *closed* — a finite, well-chosen 150 that covers every pattern a fresher gets asked. The failure mode isn't the list being too small; it's starting it three times and never finishing.

> **150 problems genuinely retained beats 400 seen once.** This is not close, and it is the whole reason this repo exists. No supplementary lists, no "one more sheet." Finish this one.

### Pass 1 — the spine (do in this order)

Order matters: each block depends on the one above it. Blocked practice within a section, then mix.

| # | NC150 Section | Qs | The pattern in one line |
|---|---|---|---|
| 1 | Arrays & Hashing | 9 | Trade memory for time — a dict kills a nested loop |
| 2 | Two Pointers | 5 | Sorted input? Walk from both ends |
| 3 | Sliding Window | 6 | Grow right, shrink left, never look back |
| 4 | Stack | 7 | When the answer depends on "the last unresolved thing" |
| 5 | Binary Search | 7 | Halve a *sorted space* — including the answer space itself |
| 6 | Linked List | 11 | Pointers only — draw it before you code it |
| 7 | Trees | 15 | Almost always recursion: base case, recurse, combine |

**Checkpoint:** these seven are ~60 problems and cover the majority of fresher screens. Do not start Pass 2 until Pass 1 is retained cold.

### Pass 2 — the differentiators

| # | NC150 Section | Qs | The pattern in one line |
|---|---|---|---|
| 8 | Tries | 3 | Prefix problems — the tree *is* the dictionary |
| 9 | Heap / Priority Queue | 7 | "Top k" or "smallest so far" → heap |
| 10 | Backtracking | 9 | Choose → explore → **un-choose** |
| 11 | Graphs | 13 | BFS = shortest/levels, DFS = explore/components |
| 12 | Advanced Graphs | 6 | Dijkstra, Union-Find, MST |
| 13 | 1-D DP | 12 | Define `dp[i]` in English *before* writing code |
| 14 | 2-D DP | 11 | Two changing inputs → grid of subproblems |
| 15 | Greedy | 8 | Locally best = globally best (and prove why) |
| 16 | Intervals | 6 | Sort by start or end — that's usually the whole trick |
| 17 | Math & Geometry | 8 | Matrix ops, digit tricks — pattern-spotting, not theory |
| 18 | Bit Manipulation | 7 | XOR cancels pairs; `n & (n-1)` clears the lowest set bit |

**Total: 150.** That's the finish line. Beyond it: revisit, don't extend.

### The rule that makes NC150 work

The list is *the* trap for someone who forgets: 150 problems solved over 4 months means Section 1 is dead by the time you reach Section 18. So:

- Every problem you solve enters `ledger.md` **by pattern**, and comes back at +1 / +3 / +7 / +16 / +35 days.
- A problem counts as done when you can **re-derive it cold** — not when you've read the solution and nodded.
- Weekly: 6 problems pulled from *finished* sections, **unlabelled**. Identifying the pattern is the skill; NeetCode's own section headers give it away for free, which is exactly why they must be stripped at review time.

### Python you must know cold

Your language is a tool you'll be judged on. These are the ones that show up:

| Area | Know without thinking |
|---|---|
| Complexity | `list` append/pop O(1), pop(0)/insert O(n) · `dict`/`set` lookup O(1) · slicing is O(k) and **copies** · string concat in a loop is O(n²) — use `''.join()` |
| `collections` | `deque` (the real queue/stack), `defaultdict`, `Counter` |
| `heapq` | **Min-heap only** — push `-x` for a max-heap. `heappush`, `heappop`, `heapify`, `nlargest` |
| Sorting | `sorted(x, key=lambda i: (i[1], -i[0]))` — multi-key sort, fluently |
| Recursion | `@functools.lru_cache` / `@cache` for instant memoization · default recursion limit is 1000 → convert deep DFS to iterative |
| Idioms | `enumerate`, `zip`, unpacking, comprehensions, `float('inf')`, `//` vs `/`, `divmod` |
| Gotchas | Mutable default arg (`def f(x=[])`) · `is` vs `==` · shallow vs deep copy · `[[0]*n]*m` creates **shared rows** |

**Be honest about the one real risk:** heavy DP or large-input graph problems can TLE in Python where C++ wouldn't. Fix is technique, not language — memoize, avoid quadratic string ops, use `deque` not `list.pop(0)`. Don't switch languages this close to placements; switching costs months and buys nothing an interviewer scores.

### Non-negotiables that people skip

- **Time & space complexity for every solution you write.** Stated out loud, before you code.
- **Dry-run on paper.** Interviewers watch how you trace, not just what you type.
- **Edge cases as a reflex:** empty, single element, all duplicates, negatives, overflow, null.
- **Think out loud.** A silent correct candidate loses to a talking near-correct one.

---

## 2 · CS Fundamentals

One page of retrievable answers per subject beats a textbook you read once.

### Operating Systems
Process vs thread · Process states & PCB · Context switching · CPU scheduling (FCFS, SJF, Round Robin, Priority) · Deadlock — 4 conditions, prevention vs avoidance (Banker's) vs detection · Synchronisation — race condition, critical section, mutex vs semaphore, producer-consumer, reader-writer · Memory — paging, segmentation, virtual memory, page faults, thrashing · Page replacement (FIFO, LRU, Optimal) · Fragmentation (internal vs external) · IPC (pipes, shared memory, message passing) · Multithreading & concurrency basics

### DBMS
ER model & keys (primary, candidate, foreign, composite) · **Normalization 1NF → BCNF with examples** · ACID · Transactions & concurrency control · **Isolation levels + which anomaly each allows** (dirty read, non-repeatable read, phantom) · Locking, 2PL, deadlock in DBs · **Indexing — B/B+ trees, clustered vs non-clustered, when an index hurts** · Joins (inner/outer/left/right/self/cross) · SQL vs NoSQL · CAP theorem *(awareness)*

**SQL you must be able to write cold:** joins, `GROUP BY` + `HAVING`, subqueries, correlated subqueries, window functions (`ROW_NUMBER`, `RANK`, `DENSE_RANK`), **2nd/Nth highest salary**, find duplicates, self-join for manager-employee.

### Computer Networks
OSI vs TCP/IP layers · **TCP vs UDP** · 3-way handshake + 4-way termination · Flow control vs congestion control · IP addressing, subnetting basics, NAT · DNS resolution flow · **"What happens when you type google.com and press Enter"** — the classic, know it end to end · HTTP vs HTTPS, TLS handshake basics · HTTP methods, status codes, REST principles · Cookies vs sessions vs tokens (JWT) · Load balancer, proxy vs reverse proxy · WebSockets vs polling

### OOP — heavily asked, heavily under-prepared
4 pillars with a real code example each (not definitions) · Abstract class **vs** interface — and *when* to use which · Overloading vs overriding · Static vs instance · **Composition vs inheritance** (and why "favour composition") · **SOLID, all five, with an example each** · Access modifiers · Constructors, destructors, copy constructor · Polymorphism: compile-time vs runtime, virtual functions/vtable · Exception handling

**Design patterns to actually know:** Singleton, Factory, Builder, Observer, Strategy, Adapter, Decorator.

**Python-specific OOP — expect these exact questions:**

| Concept | The Python answer |
|---|---|
| Interfaces | No `interface` keyword — use `abc.ABC` + `@abstractmethod`, or duck typing |
| Private members | No true private — `_x` is convention, `__x` triggers name mangling |
| Method overloading | **Not supported.** Use default args, `*args`, or `functools.singledispatch` |
| Multiple inheritance | Allowed — know the **MRO** and what `super()` actually does |
| Getters/setters | `@property` and `@x.setter`, not `getX()`/`setX()` |
| Method types | instance vs `@staticmethod` vs `@classmethod` |
| Dunder methods | `__init__`, `__str__` vs `__repr__`, `__eq__` + `__hash__`, `__len__` |
| Also asked | Decorators, generators & `yield`, context managers, the GIL, `list` vs `tuple` mutability |

Common trap: "explain encapsulation in Python" — the honest answer is that Python enforces it by *convention*, not by the compiler. Say that. Reciting Java rules in a Python interview reads as memorised, not understood.

---

## 3 · LLD (Low-Level Design)

Given a problem, produce: classes → relationships → interfaces → design patterns used → working code for the core flow. **This is where freshers get differentiated because most don't prepare it.**

Practice these seven — they cover the whole question space:

`Parking Lot` · `Elevator System` · `BookMyShow / ticket booking` · `Splitwise` · `Tic-Tac-Toe / Chess` · `ATM` · `Rate Limiter`

**How to answer:** clarify requirements → list entities → draw class diagram → apply patterns → code the core classes → discuss extensibility. Say the trade-offs out loud.

---

## 4 · HLD (System Design) — awareness only for freshers

Don't build a system-design fortress. You need to speak intelligently about:

Load balancing · Caching (Redis, cache-aside, eviction, invalidation) · DB replication & sharding · SQL vs NoSQL choice · Message queues (Kafka/RabbitMQ, why async) · CDN · Rate limiting · Horizontal vs vertical scaling · CAP theorem · Microservices vs monolith

**Two designs to have ready:** URL shortener, and a chat application. That is enough for a fresher round.

---

## 5 · Projects & Resume

The first 10 minutes of nearly every interview.

- **2 projects, deep** > 5 projects, shallow. Depth is what gets tested.
- For each project, be able to answer instantly:
  - Why this tech stack — what did you reject and why?
  - Your **exact** contribution (not "we built")
  - The hardest bug, and how you found it
  - Architecture — draw it on a whiteboard
  - How would it break at 10× users? At 1000×?
  - What would you rebuild differently today?
- **Never write anything on the resume you can't defend.** Every line is an invitation to be questioned.
- One page. Impact with numbers. Links: GitHub, LinkedIn, deployed demo.
- Contributions to open source or a live deployed app > another CRUD clone.

---

## 6 · Aptitude & Online Assessments

The filter before any human sees you — dominant at mass recruiters.

Quantitative (percentages, ratios, time-speed-distance, work, P&C, probability) · Logical reasoning (series, puzzles, blood relations, syllogisms) · Verbal ability · Technical MCQs (output prediction, complexity, DBMS/OS trivia) · **Coding: 2–3 problems in 60–90 min**

**Practice as a simulation, weekly:** timer on, no hints, no IDE autocomplete. The skill being tested is performance under a clock, not knowledge.

---

## 7 · What each company type actually asks

| Tier | Companies | The bar |
|---|---|---|
| **Tier A — top product** | Google, Amazon, Microsoft, Atlassian, Uber, Adobe, Salesforce, Flipkart, DE Shaw, Media.net | Medium–hard DSA (2–3 rounds), strong CS fundamentals, LLD, behavioural / bar-raiser |
| **Tier B — product & unicorns** | Zomato, Swiggy, PhonePe, Razorpay, Groww, CRED, Zepto, Paytm, Postman | Easy–medium DSA, LLD, deep project grilling, CS fundamentals |
| **Tier C — service & mass hiring** | TCS (NQT/Digital), Infosys, Wipro, Accenture, Cognizant, Capgemini | Aptitude-heavy, basic coding, CS fundamentals (OOP/DBMS/OS), HR round |

**Typical product-company loop:** OA → DSA round 1 → DSA round 2 / LLD → CS fundamentals + project → HR / culture fit.

---

## 8 · Behavioural & HR

Not a formality — people get rejected here.

Tell me about yourself (60 seconds, rehearsed, not memorised-sounding) · Why this company · Strengths & weaknesses (a real weakness + what you're doing about it) · A conflict in a team project · A failure and what you learned · Where do you see yourself in 5 years · Questions **you** ask them (always have two)

**Use STAR:** Situation → Task → Action → Result. Prepare 5 stories from college projects, internships, hackathons, or team work — and reuse them across questions.

---

## 9 · Phase plan

| Phase | Focus | Output |
|---|---|---|
| **1 · Foundation** | Python fluent (`collections`, `heapq`, complexity) + **NC150 Pass 1** (sections 1–7) | Any Pass 1 problem re-derived cold |
| **2 · Core** | **NC150 Pass 2** (sections 8–18) + start CS fundamentals | Medium problems in 30–40 min |
| **3 · Depth** | Finish CS fundamentals + LLD + project polish + resume | 1-page cheat sheet per subject |
| **4 · Simulation** | Weekly timed OA · **10–15 mock interviews** · HLD awareness · HR stories | Performing under pressure, out loud |
| **Continuous** | Spaced review of everything already covered | Nothing covered is ever lost |

**The continuous row is the one that decides the outcome.** Phases 1–3 are what everyone does. Retaining phases 1–3 while doing phase 4 is what almost nobody does — and it's exactly what the `dhanashri` skill in this repo automates.

---

## 10 · How to use this repo

```bash
/dhanashri new <topic>   # build a course with retention built into its structure
/dhanashri today         # today's session: recall first, then new material
/dhanashri quiz          # cold quiz on everything due for review
/dhanashri mock          # timed mock interview + gap analysis
/dhanashri status        # what's solid, what's decaying, what's overdue
```

The method, in one line: **you never study something once, and you never re-read before you've tried to recall.**

---

## The rules that beat the content

1. **Retrieval beats rereading.** Blank page first, notes second. Always.
2. **Understood ≠ remembered.** The bar is: cold, fast, and out loud.
3. **Every mistake goes in the mistake book** and comes back in 3 days.
4. **Speak while you solve.** Interviews are verbal. Practice must be too.
5. **NeetCode 150 finished and retained beats three sheets abandoned halfway.** One list. Close it.
6. **Cut scope before you cut review.** A smaller syllabus you own beats a full syllabus you've forgotten.

---

*Effort was never the missing piece. Direction was.*
