# Exercise: Unions

## Prerequisites
- Completed previous join exercises

---

## Exercise 1: Basic Unions

### Context
UNION combines the result sets of two or more SELECT statements.
- `UNION`: Removes duplicates.
- `UNION ALL`: Keeps duplicates.

### Tasks

#### Task 1.1: The Phone Book
Create a single list of names comprising:
- All Employees
- All Department names (treat them as "contacts")
- All Project names
- Output column should be named "Contact_Or_Entity"

#### Task 1.2: Event Logs (Simulation)
Imagine we have two tables: `web_log` and `mobile_log` (we will simulate them with SELECTs).
- Query 1: Select 'Web' as source, first_name from employees where department_id = 1
- Query 2: Select 'Mobile' as source, first_name from employees where department_id = 2
- Combine them into one result set.

---

## Exercise 2: Union vs Union All

### Context
Performance and data correctness.

### Tasks

#### Task 2.1: Duplicate Hunt
1. Write a query using `UNION` to combine a list of Employee first names and Manager first names (from self-join logic).
2. Write the same query using `UNION ALL`.
3. Observe the difference in row counts. Explain why one might be faster than the other.

---

## Exercise 3: Except and Intersect

### Context
Set operations beyond simple addition.

### Tasks

#### Task 3.1: Who is NOT a Manager?
Find first names of employees who are NOT managers.
- Use `EXCEPT` (Postgres syntax for set difference).
- Hint: `SELECT first_name FROM employees` EXCEPT `SELECT ...` (subquery to get manager names or self join).

#### Task 3.2: Common Names
Find first names that appear in BOTH Department 1 and Department 2 (assuming we had duplicate names, or use the query from Task 1.2 to simulate overlap if any).
- Use `INTERSECT`.

---

## Deliverables

For each exercise, provide:
1. SQL Query
2. Comparison of UNION vs UNION ALL performance/behavior.
