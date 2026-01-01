# Exercise: Inserting Data

## Prerequisites
- Basic table creation knowledge (or use provided setup)

## Setup
Create a simple table for these exercises:

```sql
CREATE TABLE tasks (
    task_id SERIAL PRIMARY KEY,
    title VARCHAR(100) NOT NULL,
    description TEXT,
    priority VARCHAR(20) DEFAULT 'Normal',
    due_date DATE,
    is_completed BOOLEAN DEFAULT false,
    created_at TIMESTAMP DEFAULT NOW()
);
```

---

## Exercise 1: Basic Inserts

### Context
`INSERT INTO` is used to add new rows. You can specify columns explicitly or rely on order (not recommended).

### Tasks

#### Task 1.1: Explicit Columns
Insert a single task titled "Buy Groceries" with a priority of "High". Leave other fields to their defaults.
- Requirement: List columns explicitly in the INSERT statement.

#### Task 1.2: Relying on Defaults
Insert a task titled "Walk the dog". Do not provide a priority, completed status, or creation date. Let the database handle those.

#### Task 1.3: Multi-Row Insert
Insert three tasks in a single SQL statement:
1. "Wash car" (Low priority)
2. "Pay bills" (High priority, due '2025-05-01')
3. "Call Mom" (Normal priority)

---

## Exercise 2: Inserting from Queries

### Context
You can insert data *from* another table. This is powerful for archiving or restructuring data.

### Tasks

#### Task 2.1: The Archive
1. Create a table `tasks_archive` with the same structure as `tasks` (or use `CREATE TABLE tasks_archive AS TABLE tasks WITH NO DATA`).
2. Write a query to insert ALL completed tasks from `tasks` into `tasks_archive`. (First update one task to be completed so you have data to move).

---

## Exercise 3: Handling Conflicts (Intro)

### Context
What happens if you violate a constraint?

### Tasks

#### Task 3.1: The Constraint Violation
Try to insert a task with `NULL` as the title.
- What error do you get?
- Why is `SERIAL` useful for the `task_id`?

---

## Deliverables

For each exercise, provide:
1. SQL Query
2. Observation of the result (e.g., "3 rows inserted")
