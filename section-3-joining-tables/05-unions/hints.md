# Hints: Unions

## Exercise 1 Hints

### Task 1.1: Phone Book

<details>
<summary>Hint</summary>

`SELECT first_name as name FROM employees UNION SELECT department_name FROM departments ...`
Columns must match in number and compatible types.
</details>

---

## Exercise 2 Hints

### Task 2.1: Duplicate Hunt

<details>
<summary>Hint</summary>

`UNION` does an implicit SORT/UNIQUE step to remove duplicates, which costs CPU. `UNION ALL` just appends rows.
</details>
