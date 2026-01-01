# Hints: Inner Joins

## Exercise 1 Hints

### Task 1.1: Employee Departments

<details>
<summary>Hint</summary>

The common column is `department_id`.
`FROM employees e JOIN departments d ON e.department_id = d.department_id`
</details>

### Task 1.2: Project Assignments

<details>
<summary>Hint</summary>

You need to join 3 tables: `employees` -> `employee_projects` -> `projects`.
The junction table `employee_projects` is the bridge.
</details>

---

## Exercise 3 Hints

### Task 3.1: Building Mates

<details>
<summary>Hint: Eliminating duplicates</summary>

To avoid matching "A-B" and "B-A", use an inequality in the join condition:
`ON d1.location = d2.location AND d1.department_id < d2.department_id`
</details>

---

## Exercise 4 Hints

### Task 4.1: Manager Names

<details>
<summary>Hint: Aliasing</summary>

Treat the table as two separate entities:
`FROM employees staff JOIN employees boss ON ...`
What is the relationship? The staff's `manager_id` matches the boss's `employee_id`.
</details>
