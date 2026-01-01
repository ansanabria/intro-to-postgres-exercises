# Hints: Returning Data

## Exercise 3 Hints

### Task 3.2: Delete and Archive

<details>
<summary>Hint</summary>

```sql
WITH moved_rows AS (
    DELETE FROM tasks
    WHERE is_completed = true
    RETURNING *
)
INSERT INTO tasks_archive
SELECT * FROM moved_rows;
```
This moves data atomically in one statement!
</details>
