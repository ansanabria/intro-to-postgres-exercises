# Project: The Todo List Application Backend

## Overview
You are building the backend persistence layer for a new "Smart Todo" application. You need to design the data modification queries that the application API will use.

## The Data
Use the `tasks` and `projects` tables.

## Requirements

### Part 1: The "Smart Add" Feature
Write a single SQL query (or transaction) that:
1. Inserts a new task "Finish Project Report".
2. Checks if a project named "Work" exists (in a hypothetical `projects` table).
   - If yes, assign the task to that project_id.
   - If no, CREATE the "Work" project first, get its ID, and then assign the task.
   - **Constraint**: Since we haven't learned PL/pgSQL functions yet, use a CTE (Common Table Expression) to perform this "Get-Or-Create" logic in one statement.

### Part 2: Task Deduplication (Cleanup)
A bug in the frontend caused duplicate tasks to be created (same title, same due_date).
1. Write a query to identify these duplicates.
2. Write a DELETE query to remove the duplicates, keeping only the one with the *lowest* `task_id`.
   - Hint: Use a subquery or `USING` clause with self-join logic.

### Part 3: The "Snooze" Button
The user wants to "Snooze" all overdue tasks.
1. Identify tasks where `due_date` < TODAY and `is_completed` is false.
2. Update them: set `due_date` to TODAY + 3 days.
3. Return the `task_id`, old due date (if possible? maybe not in simple UPDATE), and new due date.
   - *Note*: You can't return the *old* value in a simple UPDATE RETURNING. Just return the ID and new date.

### Part 4: Atomic Archive
Build a query to Archive a project and all its tasks safely.
1. Assume we have `projects` and `tasks` (with `project_id`).
2. Move a specific project (by ID) to `projects_archive`.
3. Move all tasks belonging to that project to `tasks_archive`.
4. Delete the original records.
5. **Requirement**: Use CTEs (`WITH ...`) to do this in a single atomic command chain.

## Submission
Create `solution.sql` with the queries.
