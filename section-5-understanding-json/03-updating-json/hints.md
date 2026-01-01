# Hints: Updating JSON

## Exercise 1 Hints

### Task 1.1: Updating a Field

<details>
<summary>Hint</summary>

Path is an array of text keys: `'{name}'`.
Value must be JSONB: `'"Jane Doe"'` (double quotes needed for string).

`jsonb_set(customer_info, '{name}', '"Jane Doe"')`
</details>
