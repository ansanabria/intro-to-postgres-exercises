# Hints: Intro to Indexes

## Exercise 1 Hints

### Task 1.1: Baseline

<details>
<summary>Hint</summary>

`EXPLAIN ANALYZE` executes the query and shows timing.
Without an index, it must read 100,000 rows to find one.
</details>

### Task 1.2: Adding Index

<details>
<summary>Hint</summary>

`CREATE INDEX idx_users_email ON users_large (email);`
</details>
