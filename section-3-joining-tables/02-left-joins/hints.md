# Hints: Left Joins

## Exercise 2 Hints

### Task 2.1: Bench-warmers

<details>
<summary>Hint</summary>

`WHERE project_id IS NULL` after the left join.
If an employee has no project, the join to `employee_projects` will produce a NULL `project_id`.
</details>

---

## Exercise 4 Hints

### Task 4.1: The Filter Trap

<details>
<summary>Hint 1: WHERE vs ON</summary>

- `WHERE` filters rows from the *result* of the join. If `department_name` is NULL (because of the left join), `department_name = 'Engineering'` is FALSE/NULL, so the row is dropped.
- Moving the condition to the `ON` clause applies it *during* the join.

`LEFT JOIN departments d ON ... AND d.department_name = 'Engineering'`
</details>
