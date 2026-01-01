# Hints: Right Joins

## Exercise 1 Hints

### Task 1.1: Rewrite

<details>
<summary>Hint</summary>

`FROM employees LEFT JOIN departments`
is equivalent to
`FROM departments RIGHT JOIN employees`
</details>

---

## Exercise 2 Hints

### Task 2.2: The Mismatch Report

<details>
<summary>Hint</summary>

This pattern is often called "Full Outer Join with Exclusion".
`WHERE e.employee_id IS NULL OR d.department_id IS NULL`
</details>
