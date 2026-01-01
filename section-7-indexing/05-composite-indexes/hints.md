# Hints: Composite Indexes

## Exercise 1 Hints

### Task 1.1: The Phone Book Test

<details>
<summary>Hint</summary>

Order matters!
Index `(A, B)` is sorted by A, then B.
- Search A: Easy (Start of book)
- Search A & B: Easy
- Search B: Hard (B is scattered everywhere depending on A) -> No Index usage (or slow Full Index Scan).
</details>
