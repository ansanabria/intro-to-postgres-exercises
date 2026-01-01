# Hints: B-Tree Structure

## Exercise 2 Hints

### Task 2.1: Prefix Matching

<details>
<summary>Hint</summary>

B-Trees are like a phone book. You can find "Smith" easily. You cannot find "names containing 'ith'" easily without reading every page.
Postgres only uses B-Tree for `LIKE` if the pattern does NOT start with a wildcard.
*(Note: Requires C locale or `text_pattern_ops` operator class usually, but standard setup often works for simple cases)*.
</details>
