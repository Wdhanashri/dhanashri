# DBMS · Rapid Fire — your only DBMS revision file

Cover the right column. Answer out loud. 5 min for anchors, 15 for the full set.

---

## The 12 anchors

| Anchor | → |
|---|---|
| "A key is a promise of uniqueness. A foreign key is a promise about someone else." | DB-01 Keys |
| "Store a fact once, point to it from everywhere else." · *"Ek baat, ek hi jagah"* | DB-02 Normalization |
| "Normalize for correctness. Denormalize for speed." | DB-03 Denormalization |
| "Many-to-many always needs a third table." | DB-04 Relationships |
| "INNER keeps matches. OUTER keeps orphans too." | DB-05 Joins |
| "SQL runs in a different order than you write it." | DB-06 Execution order |
| "A subquery answers once. A correlated one answers per row." | DB-07 Subqueries · windows |
| "Five queries. Everything else is a variation." | DB-08 The 5 queries |
| "All or nothing · rules never break · as if alone · survives a crash." | DB-09 ACID |
| "Three ways to be lied to. Pick which you'll tolerate." · *"Jitna sakht, utna dheema"* | DB-10 Isolation |
| "A book's index — you don't read the whole book." · *"Kitaab ka index"* | DB-11 Indexing |
| "SQL for relationships. NoSQL for scale." | DB-12 SQL vs NoSQL · CAP |

---

## 40 questions, 1-line answers

### Keys & Design
| Q | A |
|---|---|
| Super vs candidate vs primary key? | Any unique set / minimal unique set / the one you chose. |
| Primary key NULL? Foreign key NULL? | Never / yes. |
| Composite key? | Primary key of two or more columns. |
| Alternate key? | A candidate key you didn't pick as primary. |
| Referential integrity? | A foreign key must point at a row that exists. |
| Delete a referenced row? | CASCADE, SET NULL, or RESTRICT. |
| Three anomalies? | Update, insert, delete. |
| 1NF? | One value per cell, no repeating groups. |
| 2NF? | 1NF + no partial dependency — only matters with a **composite** key. |
| 3NF? | 2NF + no transitive dependency. |
| The nine-word rule? | *"Depends on the key, the whole key, and nothing but the key."* |
| BCNF? | Stricter 3NF — every determinant must be a candidate key. |
| When denormalize? | Read-heavy workloads where joins are the bottleneck. |
| Many-to-many? | Junction table with a composite key of both FKs. |
| Weak entity? | Can't exist without its parent (OrderLine without Order). |

### SQL
| Q | A |
|---|---|
| INNER vs LEFT? | Only matches / all left rows + NULLs. |
| Rows in A not in B? | LEFT JOIN + `WHERE b.key IS NULL`. |
| CROSS JOIN? | Every combination, `m × n`. |
| Self-join use case? | Employee ↔ manager in one table. Use LEFT so the CEO survives. |
| Execution order? | FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT. |
| WHERE vs HAVING? | Rows before grouping / groups after. |
| Alias in WHERE? | No — SELECT runs after WHERE. Works in ORDER BY. |
| `COUNT(*)` vs `COUNT(col)`? | All rows / skips NULLs. |
| Correlated subquery? | References the outer query; runs once per outer row; slow. |
| ROW_NUMBER vs RANK vs DENSE_RANK? | Always unique / ties share then skips / ties share, no skip. |
| PARTITION BY? | Groups rows for a window function without collapsing them. |
| 2nd highest salary? | `ORDER BY DESC LIMIT 1 OFFSET 1`, or DENSE_RANK = 2. |
| Why DENSE_RANK there? | RANK skips ranks when the top is tied → returns nothing. |
| Find duplicates? | `GROUP BY col HAVING COUNT(*) > 1`. |
| `NOT IN` returning nothing? | A single NULL in the subquery kills it. Use `NOT EXISTS`. |
| DELETE vs TRUNCATE vs DROP? | Rows (rollback-able) / all rows fast, no rollback / the whole table. |
| UNION vs UNION ALL? | Removes duplicates (slower) / keeps them. |

### Transactions & Performance
| Q | A |
|---|---|
| ACID? | Atomicity, Consistency, Isolation, Durability. |
| Write-ahead log gives? | Atomicity + Durability. |
| Odd one out in ACID? | Consistency — it's your constraints, not pure DB machinery. |
| Dirty read? | Read a value that was later rolled back. |
| Non-repeatable read? | Same row, read twice, different values (UPDATE). |
| Phantom read? | Same query, different row **count** (INSERT). |
| Four isolation levels? | Read Uncommitted, Read Committed, Repeatable Read, Serializable. |
| Which blocks phantoms? | Only SERIALIZABLE. |
| Why not always SERIALIZABLE? | More locking → less concurrency → slower. |
| MySQL / Postgres defaults? | Repeatable Read / Read Committed. |
| Why B+ tree over hash? | Hash can't do ranges; B+ leaves are sorted and linked. |
| Clustered vs non-clustered? | Rows sorted by the key (one per table) / separate structure (many). |
| When does an index hurt? | Slows writes · costs storage · useless on low-cardinality columns. |
| SQL vs NoSQL scaling? | Vertical vs horizontal. |
| BASE? | Basically Available, Soft state, Eventual consistency — NoSQL's answer to ACID. |
| CAP — the honest version? | Partition tolerance isn't optional; you choose C or A **during** a partition. |
| CP vs AP example? | Banking / social feed. |

---

## The 6 answers to have word-perfect

1. **Normalization** — three anomalies first, then 1/2/3NF, then the nine-word rule.
2. **1NF/2NF/3NF with an example** — use the student/department table.
3. **ACID** — with the ₹500 transfer.
4. **Isolation levels** — anomalies, then the staircase, then the speed trade-off.
5. **Indexing** — B+ tree, clustered vs not, **and when it hurts**.
6. **2nd highest salary** — both versions, and why DENSE_RANK.

---

## The 5 queries — write these by hand, not by reading

```sql
-- 1. Nth highest
SELECT * FROM (SELECT name, salary, DENSE_RANK() OVER (ORDER BY salary DESC) r
               FROM employee) t WHERE r = 2;

-- 2. duplicates
SELECT email, COUNT(*) FROM users GROUP BY email HAVING COUNT(*) > 1;

-- 3. delete duplicates, keep one
DELETE FROM users WHERE id NOT IN (SELECT MIN(id) FROM users GROUP BY email);

-- 4. earning more than their manager
SELECT e.name FROM employee e JOIN employee m ON e.manager_id = m.id
WHERE e.salary > m.salary;

-- 5. top earner per department
SELECT * FROM (SELECT name, dept, salary,
               RANK() OVER (PARTITION BY dept ORDER BY salary DESC) r
               FROM employee) t WHERE r = 1;
```

---

## If you have 5 minutes before an interview

Read the **12 anchors** out loud, then write query #1 from memory.
