# Exercise: Returning Data

## Prerequisites
- Completed Insert/Update/Delete exercises

---

## Exercise 1: Returning from Insert

### Context
When using `SERIAL` keys or default values, you often want to know what ID was assigned immediately after inserting.

### Tasks

#### Task 1.1: Get the ID
Insert a new task "Learn SQL" and return the generated `task_id` and the `created_at` timestamp.

---

## Exercise 2: Returning from Update

### Context
Verify what you changed without running a separate SELECT.

### Tasks

#### Task 2.1: The Verification
Update all tasks with priority 'Low' to 'Normal'.
- Return the `task_id` and the `title` of every task that was modified.

---

## Exercise 3: Returning from Delete

### Context
Archive data as you delete it.

### Tasks

#### Task 3.1: The Deleted Record
Delete the task "Walk the dog".
- Return the entire row that was deleted.

#### Task 3.2: Delete and Archive (CTE)
**Challenge**: Use a Common Table Expression (CTE) to:
1. DELETE all completed tasks.
2. RETURNING the deleted rows.
3. INSERT those returned rows into `tasks_archive`.
- Hint: `WITH deleted_rows AS (DELETE ... RETURNING *) INSERT INTO ... SELECT * FROM deleted_rows`

---

## Deliverables

For each exercise, provide:
1. SQL Query
2. Sample output
