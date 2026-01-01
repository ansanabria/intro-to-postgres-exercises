# Exercise: Characteristics of Indexes

## Prerequisites
- Intro to Indexes

---

## Exercise 1: Index Overhead

### Context
Indexes make reads faster but writes slower. Every INSERT/UPDATE/DELETE must also update the index.

### Tasks

#### Task 1.1: The Cost of Indexing
1. Create a table `heavy_write` with one column `val INTEGER`.
2. Time an insert of 100,000 rows.
3. Add 5 indexes to that column (yes, duplicate indexes for testing).
4. Time the insert again.
5. Explain the observation.

---

## Exercise 2: Partial Indexes

### Context
Index only a subset of rows to save space.

### Tasks

#### Task 2.1: The Active User Index
We often query active users, but rarely inactive ones.
1. Create a table `users_status` (id, email, is_active).
2. Create an index on `email` WHERE `is_active = true`.
3. Check `EXPLAIN` for searching an active user vs an inactive user. Does the index get used for inactive users?

---

## Deliverables

For each exercise, provide:
1. SQL Query
2. Timing observations
