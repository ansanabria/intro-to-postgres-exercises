# Exercise: Upserting Data

## Prerequisites
- Completed previous exercises
- `tasks` table

---

## Exercise 1: ON CONFLICT DO NOTHING

### Context
Sometimes you want to insert a row, but if it already exists (duplicate key), just ignore it and don't throw an error.

### Setup
Ensure `title` has a unique constraint for this exercise (or use task_id).
```sql
ALTER TABLE tasks ADD CONSTRAINT unique_title UNIQUE (title);
```

### Tasks

#### Task 1.1: The Safe Insert
Try to insert a task titled "Buy Groceries" again.
- Use `ON CONFLICT DO NOTHING`.
- Result should be no error, but 0 rows inserted.

---

## Exercise 2: ON CONFLICT DO UPDATE

### Context
This is the true "Upsert" (Update or Insert). If it exists, update it; if not, insert it.

### Tasks

#### Task 2.1: The Sync
Imagine a sync process sends you the task "Buy Groceries" with a new description "Buy Milk and Eggs".
- Write a query that inserts this task.
- If "Buy Groceries" already exists, UPDATE its description to the new one.
- **Requirement**: Use the `EXCLUDED` table to reference the new data values.

---

## Deliverables

For each exercise, provide:
1. SQL Query
2. Explanation of what `EXCLUDED` represents in the query.
