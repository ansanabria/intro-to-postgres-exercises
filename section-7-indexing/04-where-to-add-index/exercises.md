# Exercise: Where to Add Index

## Prerequisites
- Understanding B-Trees

---

## Exercise 1: High Selectivity

### Context
Indexes are best for "High Selectivity" columns (columns where the value identifies a small percentage of rows).

### Tasks

#### Task 1.1: Boolean Indexing
1. Create table `audit_log` with `is_success BOOLEAN`.
2. Fill it with 50% true, 50% false.
3. Index `is_success`.
4. Run a query `WHERE is_success = true`.
5. Does Postgres use the index? (Likely not - Seq Scan is faster than reading 50% of the index + random heap access).

#### Task 1.2: High Selectivity
1. Add a column `error_code` where 99% are NULL and 1% are specific codes.
2. Index `error_code`.
3. Query `WHERE error_code = 'ERR_1'`.
4. Does it use the index?

---

## Exercise 2: Foreign Keys

### Context
Foreign Keys are NOT indexed by default in Postgres.

### Tasks

#### Task 2.1: The Missing Link
1. Join `users_large` to another table `orders` on `user_id`.
2. Without an index on `orders.user_id`, check the JOIN performance.
3. Add the index and compare.

---

## Deliverables

For each exercise, provide:
1. SQL Query
2. Explanation of "Selectivity"
