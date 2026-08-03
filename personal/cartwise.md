# CartWise — the deep defence

**~70 min to build. Then 3 minutes before every interview.**

> **This is your only project on the resume, so it has to hold under pressure.** The good news: it's genuinely rich — payments, maps, an LLM, OCR, auth, caching. There's more to talk about here than most freshers have.
>
> **The bar:** draw the architecture on a whiteboard, name every choice you made, and say what you'd do differently. Not "know every line."

---

## ⓪ Pretest — 3 min. **Write a guess.**

1. Draw CartWise's architecture from memory, right now, before reading on.
2. Which single component would break first if 10,000 people used it tomorrow?

---

## ① The 60-second version

> *"CartWise is a full-stack grocery application. The core idea is that you scan a bill, it extracts the items with OCR, and then it gives you health-aware product recommendations using an LLM. It also finds nearby stores through the Google Maps API and handles payment through Razorpay.*
>
> *Frontend is React. Backend is FastAPI in Python, with Supabase — which is Postgres — for the database and auth. I did JWT and OTP for authentication, and added response caching so the LLM and Maps calls weren't repeated for the same query."*

**Then stop and let them pick.** You've just named six threads; let them choose which to pull.

---

## ② The architecture — draw this

**They will ask you to draw it, or you should offer.** Practise it until it takes 30 seconds on paper.

```
  ┌─────────┐
  │  React  │  user uploads a bill / searches / pays
  └────┬────┘
       │  REST (JSON)
  ┌────▼──────────────────┐
  │      FastAPI          │
  │  ┌─────────────────┐  │      ┌──────────────┐
  │  │ auth  JWT + OTP │  │      │  Grok LLM    │  health analysis,
  │  ├─────────────────┤  │─────►│              │  recommendations
  │  │ OCR   bill scan │  │      └──────────────┘
  │  ├─────────────────┤  │      ┌──────────────┐
  │  │ cache           │──┼─────►│ Google Maps  │  nearby stores
  │  └─────────────────┘  │      └──────────────┘
  └────┬──────────────────┘      ┌──────────────┐
       │                         │  Razorpay    │  payments
  ┌────▼──────────┐              └──────────────┘
  │   Supabase    │
  │  (PostgreSQL) │  users · products · orders · scanned bills
  └───────────────┘
```

> ✍️ **Blank page, 4 min.** Draw it from memory. Label every arrow with *what* travels along it.

---

## ③ The questions they will actually ask

### Q · "Why FastAPI and not Django or Flask?"
> *"FastAPI is async by default, which mattered because several of my endpoints wait on external APIs — the LLM and Maps calls are slow and I didn't want them blocking. It also generates OpenAPI docs automatically, which made testing easier while I was building. Django would have given me an admin panel and an ORM I didn't need for this."*

**Have a real trade-off ready**, not just praise. *"Django would have been better if I'd needed an admin interface"* is a stronger answer than a list of FastAPI features.

### Q · "Why Supabase rather than plain Postgres?"
> *"It's Postgres underneath, so I still get relational data and SQL. It gave me hosted auth and instant APIs so I didn't have to build user management from scratch — for a student project that saved a lot of time. The trade-off is a dependency on their platform."*

### Q · "Walk me through what happens when a user scans a bill."
**This is the flagship question. Rehearse it as a sequence.**
```
1. React uploads the image to a FastAPI endpoint
2. auth middleware validates the JWT
3. OCR extracts the text → parse into item lines
4. items matched against products in the DB
5. the item list goes to the LLM for health analysis / recommendations
6. cache the LLM response keyed on the item set
7. return the structured result to the frontend
```
**Then volunteer a weakness:** *"OCR on a crumpled or badly-lit bill is where it's least reliable — that's the part I'd improve first."* Naming your own weak point before they find it is a strong move.

### Q · "How does your authentication work?"
> *"OTP for verifying the user at sign-in, then a JWT issued on success. The token goes in the Authorization header on subsequent requests, and FastAPI validates it as a dependency on the protected routes."*

**Follow-ups to have ready:**
- **"Why JWT and not sessions?"** → stateless, so the server stores nothing; scales across instances. **Trade-off: you can't revoke a JWT before it expires** — mention this, it's the follow-up.
- **"Where do you store the token on the client?"** → say honestly what you did. The safest is an httpOnly cookie; `localStorage` is common but vulnerable to XSS. **If you used `localStorage`, say so and say you know the trade-off** — that's better than guessing.
- **"What's in the token?"** → user id, expiry, and a signature. **Never anything secret — a JWT is signed, not encrypted.**

### Q · "You mentioned caching. What did you cache and how did you invalidate it?"
> *"Mainly the LLM and Maps responses — they're slow and expensive, and the same query repeats. I keyed on the request parameters."*

**Then the honest part:** invalidation is where student projects are weakest. If you used a TTL, say so. If you didn't handle invalidation properly, say **that**:
> *"I used a time-based expiry. Proper invalidation on data change is something I'd add — right now stale data is possible for the length of the TTL."*

**That answer scores better than pretending.** Interviewers are testing whether you know what you *didn't* solve.

### Q · "How did you integrate payments? What about failures?"
> *"Razorpay — create an order server-side, the client completes payment, and then verify the signature on the callback before marking anything paid."*

**The question underneath:** *"what if the payment succeeds but your server never hears about it?"* Have a view:
> *"That's why you verify server-side rather than trusting the client, and why you'd want a webhook plus a reconciliation check rather than relying on the redirect alone."*

**Never say you trusted the frontend to confirm a payment.** That's the one wrong answer here.

### Q · "How would you scale this to a million users?"
**Use the four sentences from `../hld.md`:**
```
1. WHERE IT BREAKS   "the DB and the external API calls — the LLM
                      is the slowest thing in the request path"
2. THE CHEAP FIX     "cache aggressively; most product lookups repeat"
3. THE NEXT FIX      "read replicas, a load balancer, multiple
                      stateless FastAPI instances"
4. THE HONEST LIMIT  "move the LLM analysis onto a queue so the user
                      isn't waiting on it — and shard only if forced"
```
**Point 4 is the best one here** — the LLM call is a textbook case for async work, and saying so unprompted is exactly the D-level answer.

### Q · "What was the hardest part?"
> ________________________________________________

*Fill this in yourself. Pick something technical and specific, and say how you diagnosed it — the diagnosis is what's being scored, not the bug.*

### Q · "What would you do differently?"
> ________________________________________________

*Strong candidates: proper cache invalidation · tests · error handling around third-party APIs · a queue for the slow LLM path · rate limiting.*
*Have **two**. "Nothing" is the worst possible answer — it reads as either dishonest or incurious.*

---

## ④ The traps

| They ask | Don't | Do |
|---|---|---|
| "Did you build this alone?" | overstate | Say exactly what **you** built. "I did the backend and the integrations" is fine and credible. |
| "How does the LLM work?" | explain transformers badly | *"I use it through an API — I send the item list and a prompt and parse the structured response. I haven't trained a model."* |
| "How accurate is the OCR?" | invent a number | Say what you observed. "Good on clean printed bills, unreliable on crumpled ones." |
| "Show me the code" | panic | Know where things live in your own repo. **Open it once before every interview.** |
| Any "why did you choose X" | list features | Give a **trade-off**. Every choice cost you something — name it. |

---

## ⑤ Drill — 20 min

1. **Draw the architecture** from memory. 30 seconds. Three times.
2. **60-second version**, out loud, recorded.
3. **The bill-scan walkthrough**, out loud — all seven steps.
4. Five "why did you choose X" questions, cold. **Every answer must contain a trade-off.**
5. The scaling answer, four sentences.

> ✍️ **Blank page, 5 min.** The architecture diagram · the 7-step bill flow · one weakness you'd name before they ask.

---

## ⑥ Self-check

- [ ] Architecture drawn from memory in under 30 seconds
- [ ] Bill-scan flow, all 7 steps, out loud
- [ ] A **trade-off** ready for FastAPI, Supabase, JWT and caching
- [ ] The JWT revocation limitation, said unprompted
- [ ] The payment-verification answer (server-side, never trust the client)
- [ ] The scaling answer, ending on "put the LLM on a queue"
- [ ] **Both fill-in answers written** — hardest part, and what you'd change
- [ ] You opened the actual repo and can find things in it

---

## One last thing

You have **one** project, so every interviewer will go deep on it rather than broad. That's not a disadvantage — **depth is what they wanted anyway.** A candidate with five shallow projects gets caught on the second follow-up; you won't, if this file is done.

And when they ask *"anything else you've worked on?"* — that's your cue for preCICE. **The two together read as more than two projects would**, because one of them is code that someone else reviewed and shipped.

**Next: `questions.md`.**
