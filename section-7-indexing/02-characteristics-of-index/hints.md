# Hints: Characteristics of Indexes

## Exercise 2 Hints

### Task 2.1: The Active User Index

<details>
<summary>Hint</summary>

`CREATE INDEX ... WHERE is_active = true;`
The query optimizer will ignore this index if your query is `WHERE is_active = false`.
</details>
