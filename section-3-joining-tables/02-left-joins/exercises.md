# Exercise: Left Joins

## Prerequisites
- Completed "Inner Joins" exercises
- The tables from the previous exercise (`employees`, `departments`, etc.)

---

## Exercise 1: Basic Left Joins

### Context
LEFT JOIN returns ALL rows from the left table, and the matching rows from the right table. If no match is found, NULLs are returned for the right table's columns.

### Tasks

#### Task 1.1: All Employees and their Departments
List ALL employees, including those who don't belong to a department.
- Columns: First Name, Last Name, Department Name
- Identify which employee has a NULL department.

#### Task 1.2: Projects and Staff
List ALL projects and the employees assigned to them.
- Columns: Project Name, Employee Name
- Requirement: Include projects that have NO employees assigned.

---

## Exercise 2: Finding "Missing" Data

### Context
Left joins are the primary way to find records that DO NOT have a match in another table (e.g., "Customers who haven't placed an order").

### Tasks

#### Task 2.1: Bench-warmers
Find employees who are NOT assigned to any project.
- Hint: Left join employees to the junction table. Filter for NULLs in the junction table.

#### Task 2.2: Empty Departments
Find departments that have NO employees.

---

## Exercise 3: Multiple Left Joins

### Context
When chaining left joins, be careful. If you LEFT JOIN table A to B, and then INNER JOIN B to C, you effectively turn the first join into an inner join (because NULLs from B won't match anything in C).

### Tasks

#### Task 3.1: Full Hierarchy
List ALL employees, their department name (if any), and their manager's name (if any).
- This requires two left joins (one for department, one for manager).

---

## Exercise 4: Conceptual Challenge

### Task 4.1: The Filter Trap
Consider this query:
```sql
SELECT e.first_name, d.department_name
FROM employees e
LEFT JOIN departments d ON e.department_id = d.department_id
WHERE d.department_name = 'Engineering';
```
1. Will this return employees with NO department?
2. How would you rewrite it to include all employees, but only show the department name if it is 'Engineering' (showing NULL for others)?

---

## Deliverables

For each exercise, provide:
1. SQL Query
2. Sample output
3. Explanation for Exercise 4
