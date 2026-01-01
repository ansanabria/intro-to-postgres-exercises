# Hints: Upserting Data

## Exercise 2 Hints

### Task 2.1: The Sync

<details>
<summary>Hint: Using EXCLUDED</summary>

`EXCLUDED` is a special temporary table containing the row you *tried* to insert.
```sql
INSERT INTO ... 
ON CONFLICT (title) 
DO UPDATE SET description = EXCLUDED.description;
```
</details>
