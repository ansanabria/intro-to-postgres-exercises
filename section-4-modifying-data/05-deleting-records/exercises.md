# Exercise: Deleting Records

## Prerequisites
- Completed previous exercises
- `tasks` table

---

## Exercise 1: Basic Deletes

### Context
`DELETE FROM` removes rows. Without a WHERE clause, it wipes the table!

### Tasks

#### Task 1.1: Single Delete
Delete the task with the title "Buy Groceries".

#### Task 1.2: Conditional Delete
Delete all tasks that were created more than 1 year ago (use `created_at`).

---

## Exercise 2: Truncate

### Context
`TRUNCATE` is a fast way to empty a table. It resets the table but keeps the structure.

### Tasks

#### Task 2.1: The Reset
Empty the `tasks_archive` table completely using TRUNCATE.
- Note: It is faster than DELETE because it doesn't scan rows or log individual deletions.

---

## Exercise 3: Delete with Joins (Using USING)

### Context
Delete rows in Table A based on a condition in Table B.
Postgres uses the `USING` clause for this.

### Tasks

#### Task 3.1: The Cleanup
Delete all tasks from the `tasks` table where the title matches a "Low" priority keyword in `project_priorities`.
- Hint: `DELETE FROM tasks t USING project_priorities pp WHERE ...`

---

## Deliverables

For each exercise, provide:
1. SQL Query
2. Explanation of TRUNCATE vs DELETE
