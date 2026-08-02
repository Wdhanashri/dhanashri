# OS · Rapid Fire — your only OS revision file

**Use this, not s1–s3.** Cover the right column. Answer out loud. 5 minutes for anchors, 15 for the full set.

---

## The 12 anchors

| Anchor | → |
|---|---|
| "Processes are separate houses. Threads are rooms in one house." | OS-01 Process vs Thread |
| "Save everything, load everything else — and the cache goes cold." | OS-02 Context switch |
| "Who runs next, and can you interrupt them?" · *"Ek truck aage, poori line peeche"* | OS-03 Scheduling |
| "Your code can't touch hardware. It has to ask." | OS-04 User/kernel mode |
| "Two threads, one variable, and the answer depends on luck." · *"Dono ne purana balance dekha"* | OS-05 Race condition |
| "Mutex is one key. Semaphore is N keys." · *"ek chabi / N chabiyan"* | OS-06 Mutex vs Semaphore |
| "You let go first. No, you let go first." · *"Tu pehle chhod"* | OS-07 Deadlock |
| "Prevent it, dodge it, detect it — or ignore it." | OS-08 Handling deadlock |
| "Small desk, many books." · *"Mez chhoti, kitaabein zyada"* | OS-09 Virtual memory |
| "Paging cuts by size. Segmentation cuts by meaning." | OS-10 Paging vs segmentation |
| "Not in RAM? Stop, fetch from disk, resume." · *"Kitaab mez pe nahi? Almari se laao"* | OS-11 Page fault · TLB |
| "More time swapping than working." · *"Kaam kam, saaman badalna zyada"* | OS-12 Thrashing |

---

## 40 questions, 1-line answers

### Process & Thread
| Q | A |
|---|---|
| Process vs thread? | Process = own memory. Threads share memory inside a process; cheaper to create and switch. |
| What do threads share? | Code, data, heap, open files. |
| What's private to a thread? | Stack, registers, program counter. |
| Why are threads cheaper? | No new address space or page tables. |
| One thread crashes — what happens? | The whole process dies. |
| What's in a PCB? | PID, state, registers, PC, memory map, open files, priority. |
| Process states? | NEW → READY ⇄ RUNNING → TERMINATED, plus RUNNING → WAITING → READY. |
| RUNNING → READY is caused by? | Time slice expiring (preemption). |
| RUNNING → WAITING? | I/O or waiting for an event. |
| Why does a context switch cost? | Save/restore registers, switch page tables, flush TLB — **and the cache goes cold**. |
| Multitasking vs multithreading? | Multitasking = many processes. Multithreading = many threads in one process. |
| Zombie process? | Finished, but its parent hasn't read the exit status yet. |
| Orphan process? | Parent died first; adopted by `init`. |

### Scheduling
| Q | A |
|---|---|
| Preemptive vs non-preemptive? | Can the OS take the CPU away mid-run — yes / no. |
| Convoy effect? | FCFS: one long job blocks everyone behind it. |
| Why can SJF starve jobs? | Short jobs keep arriving and keep jumping the queue. |
| Fix for starvation? | **Ageing** — raise priority the longer it waits. |
| RR time slice too small? | Context-switch overhead dominates. |
| Too large? | Degenerates into FCFS. |
| Which algorithm is best? | Depends: batch → SJF (throughput), interactive → RR (response time). |
| Turnaround vs waiting time? | Turnaround = completion − arrival. Waiting = turnaround − burst. |

### Concurrency
| Q | A |
|---|---|
| Race condition? | Result depends on thread timing. |
| Why isn't `x += 1` safe? | It's read-modify-write — preemptible mid-way. |
| Critical section requirements? | Mutual exclusion, progress, bounded waiting. |
| Mutex vs semaphore? | **Ownership** — only the locker may unlock a mutex. |
| Binary semaphore vs mutex? | Nearly identical, but no ownership. |
| Producer–consumer variables? | `empty` semaphore, `full` semaphore, `mutex`. |
| Lock the mutex before `wait(empty)`? | You sleep holding the lock → deadlock. |
| What is a spinlock? | Busy-waits instead of sleeping. Good only for very short waits. |

### Deadlock
| Q | A |
|---|---|
| Four conditions? | Mutual exclusion, hold and wait, no preemption, circular wait. |
| Together or separately? | **All four, simultaneously.** |
| Deadlock vs starvation? | Deadlock: nobody moves, circular. Starvation: others move, one never gets a turn. |
| Four handling strategies? | Prevention, avoidance (Banker's), detection + recovery, ostrich. |
| Easiest condition to break? | Circular wait — impose a global lock ordering. |
| Banker's algorithm? | Grant a request only if a safe sequence still exists afterwards. |
| What do real OSes do? | The ostrich algorithm — ignore it. |
| Livelock? | Threads keep changing state but make no progress. |

### Memory
| Q | A |
|---|---|
| Why virtual memory? | Run bigger than RAM · isolation · every program starts at 0. |
| Who translates addresses? | The **MMU**, in hardware, using the page table. |
| Paging vs segmentation? | Fixed-size OS chunks vs variable logical units. |
| Internal fragmentation? | Unused space *inside* an allocated block — paging's problem. |
| External fragmentation? | Enough free memory total, no single gap big enough — segmentation's. Fix: compaction. |
| What does the TLB cache? | Recent virtual→physical translations. |
| Why flush the TLB on a context switch? | New process, entirely different mapping. |
| Page fault steps? | Trap → find on disk → evict if needed → load → update table → **restart** the instruction. |
| Is a page fault an error? | No. Invalid address is (segfault). |
| Belady's anomaly? | More frames → more faults. **FIFO** only. |
| Why is OPT impossible? | It needs to know future accesses. Benchmark only. |
| Demand paging? | Load a page only when it's actually referenced. |
| Thrashing? | More time paging than executing. |
| Why does the spiral get worse? | Low CPU use makes the OS start *more* processes. |
| Fix for thrashing? | Working-set model, page-fault frequency control, or suspend processes. |

---

## The 6 answers to have word-perfect

These get asked most. Rehearse them until they're clean, then stop.

1. **Process vs thread** — separate memory vs shared; cheap to create/switch; sharing is why you need synchronisation.
2. **Why a context switch costs** — registers, page tables, TLB flush, **cold cache**.
3. **Deadlock** — four conditions, *simultaneously*; break one and it can't happen.
4. **Mutex vs semaphore** — ownership.
5. **Virtual memory** — bigger than RAM, isolation, simple addressing.
6. **Thrashing** — more paging than working, and the OS's own reaction worsens it.

---

## If you have 5 minutes before an interview

Read the **12 anchors** out loud. That's it. They pull the rest back.
