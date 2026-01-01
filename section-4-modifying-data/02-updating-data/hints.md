# Hints: Updating Data

## Exercise 3 Hints

### Task 3.1: Intelligent Updates

<details>
<summary>Hint</summary>

```sql
UPDATE tasks t
SET priority = pp.new_priority
FROM project_priorities pp
WHERE t.title ILIKE '%' || pp.keyword || '%';
```
</details>
