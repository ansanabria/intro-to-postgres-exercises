# Hints: Generated Columns from JSON

## Exercise 1 Hints

### Task 1.1: The Customer Email

<details>
<summary>Hint</summary>

```sql
ALTER TABLE orders 
ADD COLUMN email TEXT 
GENERATED ALWAYS AS (customer_info ->> 'email') STORED;
```
Note: In Postgres, generated columns must be `STORED` (computed on write), not `VIRTUAL`.
</details>
