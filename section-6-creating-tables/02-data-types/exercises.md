# Exercise: Data Types

## Prerequisites
- `CREATE TABLE` syntax

---

## Exercise 1: Choosing the Right Type

### Context
Postgres has rich types. Using the right one ensures data integrity and saves space.

### Tasks

#### Task 1.1: The Type Picker
Choose the best PostgreSQL data type for each field and explain why:
1. User's age (0-120)
2. Product price (e.g., $19.99)
3. "Is Active" status
4. A paragraph of text (blog post body)
5. A fixed-length country code (e.g., "US", "CA")
6. IP Address

#### Task 1.2: Numeric vs Integer vs Real
Create a table `math_test`:
- `val_int INTEGER`
- `val_num NUMERIC(10,2)`
- `val_real REAL`

Insert `10.5` into all of them. What happens?

---

## Exercise 2: Text Types

### Context
`CHAR(n)`, `VARCHAR(n)`, and `TEXT`.
In Postgres, `TEXT` is generally preferred unless you have a strict length constraint.

### Tasks

#### Task 2.1: Length Constraints
Create a table `users_temp` with `username VARCHAR(5)`.
Try to insert 'Alexander'. What happens?

---

## Deliverables

For each exercise, provide:
1. SQL Statements
2. Explanation of type choices
