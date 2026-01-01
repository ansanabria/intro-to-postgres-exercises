# Hints: Todo List Backend

## Part 1: The "Smart Add"

<details>
<summary>Hint</summary>

This is a classic "Get or Create" pattern.
```sql
WITH project_search AS (
    SELECT project_id FROM projects WHERE name = 'Work'
),
new_project AS (
    INSERT INTO projects (name)
    SELECT 'Work'
    WHERE NOT EXISTS (SELECT 1 FROM project_search)
    RETURNING project_id
)
INSERT INTO tasks (title, project_id)
SELECT 'Finish Report', COALESCE(
    (SELECT project_id FROM project_search),
    (SELECT project_id FROM new_project)
);
```
</details>

## Part 2: Task Deduplication

<details>
<summary>Hint</summary>

```sql
DELETE FROM tasks t1
USING tasks t2
WHERE t1.task_id > t2.task_id 
  AND t1.title = t2.title 
  AND t1.due_date = t2.due_date;
```
</details>

## Part 4: Atomic Archive

<details>
<summary>Hint</summary>

Chain CTEs:
`WITH moved_projects AS (DELETE ... RETURNING *), moved_tasks AS (DELETE ... RETURNING *) INSERT ...`
</details>
