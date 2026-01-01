# Exercise: Composite Indexes

## Prerequisites
- B-Tree basics

---

## Exercise 1: Multi-Column Indexing

### Context
An index on `(a, b)` supports queries on `a` AND queries on `a, b`. It does NOT support queries on `b` alone efficiently.

### Tasks

#### Task 1.1: The Phone Book Test
1. Create table `contacts` (first_name, last_name).
2. Create index on `(last_name, first_name)`.
3. Query `WHERE last_name = 'Smith'`. (Index used?)
4. Query `WHERE last_name = 'Smith' AND first_name = 'John'`. (Index used?)
5. Query `WHERE first_name = 'John'`. (Index used?)

---

## Exercise 2: Index-Only Scans

### Context
If all columns needed are in the index, Postgres doesn't need to visit the main table (Heap) at all.

### Tasks

#### Task 2.1: Covering Index
1. Use the composite index from Task 1.1.
2. `SELECT first_name FROM contacts WHERE last_name = 'Smith'`.
3. Check `EXPLAIN`. Do you see "Index Only Scan"?

---

## Deliverables

For each exercise, provide:
1. SQL Query
2. Yes/No answers for Task 1.1
