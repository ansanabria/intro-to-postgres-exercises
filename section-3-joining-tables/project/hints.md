# Hints: HR Analytics Suite

## Part 1: The "Org Chart" View

<details>
<summary>Hint</summary>

- `LEFT JOIN` employees (manager) to employees (staff)
- `LEFT JOIN` departments
- `LEFT JOIN` employee_projects then `GROUP BY` employee to get the count.
</details>

## Part 2: Department Workload

<details>
<summary>Hint</summary>

Start `FROM departments`.
`LEFT JOIN employees` -> `LEFT JOIN employee_projects` -> `LEFT JOIN projects`
Use `STRING_AGG(DISTINCT project_name, ', ')`
</details>

## Part 3: Project Staffing Gaps

<details>
<summary>Hint</summary>

`SUM(CASE WHEN role ILIKE '%Lead%' THEN 1 ELSE 0 END)`
</details>

## Part 4: The "Audit" Log

<details>
<summary>Hint</summary>

`SELECT 'User: ' || first_name || ' ' || last_name ... UNION ...`
</details>
