# Exercise: Updating Data

## Prerequisites
- Completed "Inserting Data"
- Populated `tasks` table

---

## Exercise 1: Basic Updates

### Context
`UPDATE` modifies existing rows. **Always check your WHERE clause!**

### Tasks

#### Task 1.1: Single Row Update
Mark the task "Walk the dog" as completed (`is_completed = true`).

#### Task 1.2: Multi-Column Update
Change the "Wash car" task: set priority to "High" AND due_date to tomorrow.

---

## Exercise 2: Bulk Updates

### Context
Updating multiple rows at once based on conditions.

### Tasks

#### Task 2.1: The Procrastinator
Move the `due_date` of ALL "High" priority tasks forward by 1 week.
- Hint: You can do date math: `due_date + INTERVAL '1 week'`.

#### Task 2.2: Reset
Set the `is_completed` status to `false` for ALL tasks created today.

---

## Exercise 3: Updating with Joins (Update from another table)

### Context
Sometimes you need to update Table A based on data in Table B.
Postgres uses a `FROM` clause in the UPDATE statement for this.

### Setup
Create a `project_priorities` table:
```sql
CREATE TABLE project_priorities (
    keyword VARCHAR(50),
    new_priority VARCHAR(20)
);
INSERT INTO project_priorities VALUES ('Buy', 'Low'), ('Call', 'High');
```

### Tasks

#### Task 3.1: Intelligent Updates
Update the `tasks` table. Set the `priority` of a task to the `new_priority` found in `project_priorities` IF the task title contains the `keyword`.
- Example: "Buy Groceries" contains "Buy", so it should become "Low" priority. "Call Mom" contains "Call", so it becomes "High".
- Hint: `UPDATE tasks SET ... FROM project_priorities WHERE ...`

---

## Deliverables

For each exercise, provide:
1. SQL Query
2. How many rows were affected?
