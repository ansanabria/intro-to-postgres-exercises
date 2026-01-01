# Hints: Deleting Records

## Exercise 3 Hints

### Task 3.1: The Cleanup

<details>
<summary>Hint</summary>

```sql
DELETE FROM tasks t
USING project_priorities pp
WHERE t.title ILIKE '%' || pp.keyword || '%' 
  AND pp.new_priority = 'Low';
```
</details>
