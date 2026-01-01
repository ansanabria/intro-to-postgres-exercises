# Hints: Generated Columns

## Exercise 1 Hints

### Task 1.1: Full Name

<details>
<summary>Hint</summary>

`full_name TEXT GENERATED ALWAYS AS (first_name || ' ' || last_name) STORED`
</details>
