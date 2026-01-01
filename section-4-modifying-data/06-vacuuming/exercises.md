# Exercise: Vacuuming

## Prerequisites
- Completed Modification exercises
- Understanding that DELETE doesn't physically remove data immediately

---

## Exercise 1: Understanding MVCC

### Context
Postgres uses Multi-Version Concurrency Control (MVCC). When you update/delete, old row versions ("dead tuples") stay on disk until vacuumed.

### Tasks

#### Task 1.1: Dead Tuples
1. Run a query to count rows in `tasks`.
2. Delete half the rows.
3. Run `VACUUM` (standard) on the table.
4. Explain what happened to the dead tuples. Did the file size on disk necessarily shrink?

#### Task 1.2: Vacuum Full
1. Run `VACUUM FULL tasks`.
2. Explain how this differs from standard `VACUUM`. Why might you NOT want to run this on a production database during peak hours?

---

## Deliverables

For each exercise, provide:
1. SQL Commands used
2. Written explanation of MVCC, Dead Tuples, and the difference between VACUUM and VACUUM FULL.
