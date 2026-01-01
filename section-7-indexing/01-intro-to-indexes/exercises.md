# Exercise: Introduction to Indexes

## Prerequisites
- Basic tables with data
- `EXPLAIN` (we'll introduce it)

## Setup
Create a large table (or simulate one) to see index effects.
```sql
CREATE TABLE users_large (
    id SERIAL PRIMARY KEY,
    email TEXT,
    name TEXT
);
-- Insert 100,000 rows (approx)
INSERT INTO users_large (email, name)
SELECT 'user_' || i || '@example.com', 'User ' || i
FROM generate_series(1, 100000) AS i;
```

---

## Exercise 1: To Scan or To Seek?

### Context
Without an index, Postgres performs a "Sequential Scan" (reads every row). With an index, it performs an "Index Scan" (jumps to the data).

### Tasks

#### Task 1.1: The Baseline
Run `EXPLAIN ANALYZE SELECT * FROM users_large WHERE email = 'user_50000@example.com';`.
- Record the "Execution Time" and the Scan Type (Seq Scan).

#### Task 1.2: Adding the Index
1. Create an index on `email`.
2. Run the same query again.
3. Compare the Execution Time and Scan Type.

---

## Exercise 2: Unique Indexes

### Context
Indexes can also enforce uniqueness.

### Tasks

#### Task 2.1: Enforcing Integrity
1. Try to insert a duplicate email. (It should succeed right now).
2. Create a UNIQUE INDEX on email. (This might fail if you just inserted a duplicate - delete it first).
3. Try to insert a duplicate again.

---

## Deliverables

For each exercise, provide:
1. SQL Query
2. Performance comparison numbers (e.g., "Seq Scan: 15ms, Index Scan: 0.05ms")
