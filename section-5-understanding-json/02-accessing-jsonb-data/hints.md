# Hints: Accessing JSONB Data

## Exercise 3 Hints

### Task 3.1: Finding Customers

<details>
<summary>Hint</summary>

`WHERE customer_info @> '{"name": "John Doe"}'`
This is generally faster than `WHERE customer_info->>'name' = 'John Doe'` because it can use an index.
</details>
