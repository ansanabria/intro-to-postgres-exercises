# Hints: Orphaned Data

## Exercise 1 Hints

### Task 1.1: Invalid Departments

<details>
<summary>Hint 1: Using Left Join</summary>

`FROM employees e LEFT JOIN departments d ON ... WHERE d.id IS NULL AND e.dept_id IS NOT NULL`
</details>

<details>
<summary>Hint 2: Using NOT EXISTS</summary>

`WHERE NOT EXISTS (SELECT 1 FROM departments d WHERE d.id = e.dept_id)`
</details>

---

## Exercise 2 Hints

### Task 2.1: Cross Join

<details>
<summary>Hint</summary>

`FROM employees CROSS JOIN projects`
OR
`FROM employees, projects` (Old style syntax, but effective here)
</details>

### Task 2.2: Unassigned Combinations

<details>
<summary>Hint</summary>

1. Generate all pairs (Cross Join)
2. Left Join to `employee_projects`
3. Filter where `employee_projects.role` IS NULL
</details>
