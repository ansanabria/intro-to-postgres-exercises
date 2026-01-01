# Hints: Where to Add Index

## Exercise 1 Hints

### Task 1.1: Boolean Indexing

<details>
<summary>Hint</summary>

If you select > 5-10% of the table, Postgres often prefers a Sequential Scan. Indexes are for finding needles in haystacks, not for reading half the haystack.
</details>
