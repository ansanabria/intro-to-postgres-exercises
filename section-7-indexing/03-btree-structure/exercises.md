# Exercise: B-Tree Structure

## Prerequisites
- Basic indexing

---

## Exercise 1: Range Queries

### Context
B-Trees are excellent for equality (`=`) and ranges (`<`, `>`, `BETWEEN`).

### Tasks

#### Task 1.1: The Range Test
1. Using `users_large` (from previous exercises), query for IDs `BETWEEN 1000 AND 2000`.
2. Check `EXPLAIN`. Does it use the Primary Key index (which is a B-Tree)?

#### Task 1.2: Sorting
1. Query `SELECT * FROM users_large ORDER BY email LIMIT 10`.
2. Check `EXPLAIN`. Does it use the index on `email` to avoid a "Sort" step? (B-Trees store data sorted!).

---

## Exercise 2: Prefix Matching

### Context
B-Trees support "Starts With" (Left-anchored) pattern matching.

### Tasks

#### Task 2.1: Like 'User%'
1. Query `WHERE email LIKE 'user_50%'`.
2. Check if the index is used.
3. Query `WHERE email LIKE '%50%'` (Contains).
4. Check if the index is used. Explain why not.

---

## Deliverables

For each exercise, provide:
1. SQL Query
2. EXPLAIN output analysis
