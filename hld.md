# HLD — awareness level, one file

**~90 minutes total. Read once, then only ever use the drill at the bottom.**

---

## Be clear about the scope

You will almost certainly **not** get a system design round as a fresher. What you *will* get is this, five minutes into your project discussion:

> *"Okay — so how would you scale this if you had a million users?"*

That's the question this file exists for. You don't need to design Netflix. You need to **not go blank**, name four or five components, and say why each one is there.

**Everything below fits on one page and covers it.** Anything more is time stolen from DSA, which is the round that actually decides your offer.

---

## ① THE ONE DIAGRAM

**Anchor:** *"Every system is the same line: user → edge → servers → cache → database."*

Learn this and every component question becomes *"where on this line does it sit?"*

```
                                        ┌──────────┐
 user ──► DNS ──► CDN ──►  LOAD    ────►│ server 1 │──► CACHE ──► DB primary
                          BALANCER      │ server 2 │      │           │ writes
                  (static files)        │ server 3 │      └─miss─►    │
                                        └────┬─────┘              replicas
                                             │                    (reads)
                                             │ slow work
                                             ▼
                                       MESSAGE QUEUE ──► workers
                                       (email, reports, video encoding)
```

> ✍️ **Redraw this from memory before reading on.** Two minutes. If you can draw this line and label every box, you have 80% of what a fresher is asked.

---

## ② The components — one line each

| Component | What it does | Say this |
|---|---|---|
| **Vertical scaling** | bigger machine | "simple, but there's a ceiling and a single point of failure" |
| **Horizontal scaling** | more machines | "what you actually do — needs a load balancer and stateless servers" |
| **Load balancer** | spreads traffic across servers | "round robin or least-connections, plus health checks to drop dead servers" |
| **CDN** | static files served from a nearby edge | "images, CSS, JS — cuts latency and takes load off the origin" |
| **Cache (Redis)** | keeps hot data in memory | "reads are ~100× faster than the DB; the hard part is invalidation" |
| **Replication** | copies of the DB | "writes to primary, reads from replicas — most apps are read-heavy" |
| **Sharding** | splits data across DBs | "when one machine can't hold it. Cross-shard joins become painful." |
| **Message queue** | work done later, not now | "the user shouldn't wait for an email to send" |
| **Rate limiting** | caps requests per user | "protects against abuse and accidental loops" |
| **Stateless servers** | no session data on the server | "so any server can serve any request — this is what makes scaling possible" |

**The Gotcha:** *stateless* is the one people miss, and it's the one that makes the rest work. If server 2 holds your login session, the load balancer can't send you to server 3. Sessions go in Redis or a token — never on the server.

**Recall:** *Why must servers be stateless before you can scale horizontally?*

---

## ③ Caching — the one worth 5 extra minutes

**Anchor:** *"Check cache. Miss? Go to DB, then put it in the cache."*

```
read:   app ──► cache ──hit──► return                    (fast)
                  │
                miss──► DB ──► store in cache ──► return  (slow, once)
```
That's **cache-aside**, and it's the pattern you should name.

```
EVICTION      cache is full → throw something out → LRU (least recently used)
INVALIDATION  data changed → the cache is now LYING
              fixes: TTL (expire after N seconds) · delete the key on write
```

**The line to say:** *"There are only two hard problems in computing — cache invalidation and naming things."* Then explain it: a cache is a copy, and copies go stale. TTL is the cheap fix; deleting the key on write is the correct one.

**Recall:** *What are the two hard parts of caching?*

---

## ④ The four trade-offs you'll actually be asked

**SQL vs NoSQL**
> *"SQL when the data is relational and I need ACID — payments, orders. NoSQL when the schema is loose or I need horizontal scale — logs, feeds, catalogues."*

**Monolith vs microservices**
> *"Start with a monolith. It's simpler and faster to build. Split into services when teams or scaling needs actually diverge — microservices trade simplicity for independent deployment."*
>
> **Freshers who say "microservices" reflexively get caught here.** Preferring the monolith first is the mature answer.

**Sync vs async**
> *"If the user needs the result now, sync. If not — emails, reports, video processing — put it on a queue and respond immediately."*

**CAP**
> *"During a network partition you choose consistency or availability. Partition tolerance isn't optional — networks fail. Banking picks CP; a social feed picks AP."*
>
> Saying *"pick 2 of 3"* is the sloppy version. The above is the correct one.

---

## ⑤ Numbers worth having

You'll never be asked to compute precisely. You *will* sound credible if these are roughly right.

```
memory read     ~100 ns          │   1 million users
SSD read        ~100 µs          │   × 10 requests/day
network, same DC ~0.5 ms         │   = 10M req/day ≈ 120 req/sec average
network, cross-country ~50 ms    │   peak ≈ 3-5× average
DB query        ~1-10 ms         │
                                 │   1 KB × 10M = 10 GB/day
cache ≈ 100× faster than disk    │   × 365 ≈ 3.6 TB/year
```

**The move:** when asked to estimate, say your assumptions out loud — *"assume a million users, ten requests each per day"* — then do simple arithmetic. **Nobody checks the number. They check that you have a method.**

---

## ⑥ One worked design — URL shortener

The classic, and it exercises everything above. **Know this one cold; the shape transfers.**

**1 · Clarify** → How many URLs/day? Custom aliases? Do links expire? Do we need analytics?
*Assume: 10M writes/day, 100:1 read:write, 7-char codes, no expiry.*

**2 · The core problem** — long URL → short code, and back.
```
POST /shorten  {url}  →  {short: "abc1234"}
GET  /abc1234         →  301 redirect to the long URL
```

**3 · Generating the code**
```
OPTION A  hash(url) → take 7 chars     ← collisions possible, must check
OPTION B  counter + base62 encode      ← no collisions, but predictable & sequential
          62^7 ≈ 3.5 trillion codes — plenty
```
Say the trade-off. **That's the whole question** — everything else is plumbing.

**4 · Storage** → key-value, `short_code → long_url`. **NoSQL fits**: no joins, no relations, pure lookup by key.

**5 · Scale it**
```
read-heavy (100:1)  →  CACHE the hot codes in Redis. Huge win.
                    →  read replicas for the DB
                    →  load balancer in front of the app servers
                    →  shard by short_code once one DB isn't enough
```

**6 · Pre-empt the follow-up** — *"Analytics? I'd fire a click event onto a message queue so the redirect stays fast."*

> ✍️ **Blank page, 6 min.** Draw the whole thing from memory: the two endpoints, the two code-generation options with their trade-off, where the cache sits.

---

## ⑦ The question you'll actually get

> *"How would you scale your project?"*

Answer it in this order, every time — **four sentences, forty seconds**:

```
1. WHERE IT BREAKS   "right now everything is one server and one DB,
                      so the DB is the first bottleneck"
2. THE CHEAP FIX     "I'd add a cache for the hot reads"
3. THE NEXT FIX      "then read replicas, and a load balancer across
                      multiple stateless app servers"
4. THE HONEST LIMIT  "sharding if the data outgrows one machine —
                      but I'd only do that when I actually had to"
```

**That last sentence is the one that scores.** Knowing when *not* to add complexity is exactly what separates someone who understands systems from someone reciting components.

---

## ⏱ RAPID FIRE — notes closed, out loud, 30 seconds each

```
 1.  Draw the request path, every box labelled.
 2.  Vertical vs horizontal scaling — one line each.
 3.  Why must servers be stateless to scale horizontally?
 4.  Where do sessions live instead?
 5.  Two load-balancing algorithms?
 6.  What does a CDN actually serve?
 7.  Explain cache-aside.
 8.  Two hard parts of caching?
 9.  What is LRU eviction?
10.  Replication — where do writes go? Reads?
11.  When do you shard, and what gets harder?
12.  Give one thing that belongs on a message queue.
13.  SQL or NoSQL for a URL shortener — and why?
14.  Monolith or microservices to start — and why?
15.  CAP — the correct phrasing, not "pick 2 of 3".
16.  Roughly how much faster is cache than disk?
17.  1M users × 10 requests/day ≈ how many req/sec?
18.  URL shortener — the two ways to make a code, and the trade-off?
19.  "How would you scale your project?" — your four sentences.
20.  Why would you *refuse* to add sharding?
```

<details><summary>Answers</summary>

1. user → DNS → CDN → load balancer → servers → cache → DB (primary + replicas); queue hanging off the servers.
2. Bigger machine, has a ceiling / more machines, needs a load balancer.
3. Because any server must be able to serve any request — the LB can't guarantee you reach the same one.
4. Redis, or a signed token the client carries (JWT).
5. Round robin, least connections. (Also IP hash.)
6. Static files — images, CSS, JS — from a nearby edge.
7. Check cache → on miss read the DB, store it in the cache, return.
8. Invalidation (stale copies) and eviction (what to throw out when full).
9. Evict the least recently used entry.
10. Writes → primary. Reads → replicas.
11. When one machine can't hold the data. Cross-shard joins and transactions get painful.
12. Emails, notifications, report generation, video encoding, analytics events.
13. NoSQL — pure key-value lookup, no relations, no joins.
14. Monolith — simpler, faster to build. Split only when needs actually diverge.
15. During a partition you choose C or A. Partition tolerance isn't optional.
16. ~100×.
17. ~120/sec average, peak 3–5× that.
18. Hash-and-truncate (collisions possible) vs counter+base62 (no collisions, predictable).
19. Where it breaks → cache → replicas + LB → sharding only if forced.
20. Because it isn't needed yet, and it makes joins and transactions much harder. **Complexity you don't need is a cost, not a credential.**
</details>

**Score:** __/20. Under 16 → redo the drill in 3 days. Over 16 → you're done; keep it alive below.

---

## Keeping it — 5 minutes a month

Draw **the one diagram** from memory and say the **four sentences** for scaling your project. That's it.

Don't study HLD further unless a company explicitly says they'll test it. At your level this file is the whole return; everything beyond it competes with DSA, and DSA is what decides the offer.
