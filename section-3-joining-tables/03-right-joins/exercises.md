# Exercise: Right Joins and Outer Joins

## Prerequisites
- Completed Inner and Left Join exercises
- The same dataset

---

## Exercise 1: Right Joins

### Context
RIGHT JOIN is the opposite of LEFT JOIN. It returns all rows from the RIGHT table.
*Note: Most developers prefer to use LEFT JOINs for readability (reading left-to-right), but understanding RIGHT JOIN is necessary.*

### Tasks

#### Task 1.1: Rewrite with Right Join
Take the query from Left Join Task 1.1 ("All Employees and their Departments") and rewrite it using a RIGHT JOIN to achieve the **exact same result**.
- Hint: You'll need to swap the table order.

#### Task 1.2: Departments and Employees
List ALL departments, including those with no employees, using a RIGHT JOIN.
- Start with `FROM employees`...

---

## Exercise 2: Full Outer Joins

### Context
FULL JOIN returns rows when there is a match in one of the tables. It essentially combines the results of both LEFT and RIGHT joins.

### Tasks

#### Task 2.1: The Complete Picture
List ALL employees and ALL departments.
- Include employees with no department.
- Include departments with no employees.
- Columns: Employee Name, Department Name

#### Task 2.2: The Mismatch Report
Find records where EITHER:
- An employee has no department OR
- A department has no employees
But NOT records where both match.
- Hint: Use FULL JOIN with a WHERE clause checking for NULLs.

---

## Deliverables

For each exercise, provide:
1. SQL Query
2. Brief explanation of why you might choose LEFT over RIGHT join in practice.
