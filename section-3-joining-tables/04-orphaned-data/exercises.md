# Exercise: Orphaned Data

## Prerequisites
- Completed Join exercises
- The dataset

## Setup
We'll intentionally create some orphaned data (referencing a non-existent parent) to practice finding it.
Note: In a well-designed database, Foreign Key constraints prevent this. We will assume constraints are disabled or haven't been applied yet.

```sql
-- Insert an employee with a non-existent department_id
INSERT INTO employees (first_name, last_name, department_id, hire_date) 
VALUES ('Orphan', 'Annie', 999, '2023-01-01');

-- Insert a project assignment for a non-existent project
INSERT INTO employee_projects (employee_id, project_id, role)
VALUES (1, 888, 'Ghost Hunter');
```

---

## Exercise 1: Finding Orphans

### Context
"Orphans" are child records that point to a non-existent parent record. This leads to data integrity issues.

### Tasks

#### Task 1.1: Employees with Invalid Departments
Find employees whose `department_id` does not exist in the `departments` table.
- Do NOT include employees with NULL department_id (those are valid "unassigned" employees).
- Only find those pointing to an ID that doesn't exist.

#### Task 1.2: Invalid Project Assignments
Find rows in `employee_projects` that reference a non-existent `project_id`.

---

## Exercise 2: Cross Joins (The Cartesian Product)

### Context
While not strictly "orphaned data", CROSS JOIN creates every possible combination of rows. It's useful for generating reports (e.g., "Every employee for every month").

### Tasks

#### Task 2.1: The Schedule Template
Generate a list of every employee combined with every project.
- This creates a template we could use to check who is assigned to what.
- Columns: Employee Name, Project Name

#### Task 2.2: Finding Unassigned Combinations
Use the Cross Join from 2.1 and LEFT JOIN it to the actual `employee_projects` table to find all Employee-Project pairs that do NOT exist.
- This tells us "Who is NOT working on Which project".

---

## Deliverables

For each exercise, provide:
1. SQL Query
2. Explanation of the technique used (e.g., `NOT EXISTS` vs `LEFT JOIN / IS NULL`)
