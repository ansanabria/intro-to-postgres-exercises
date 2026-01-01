# Exercise: Check Constraints

## Prerequisites
- Table creation

---

## Exercise 1: Ensuring Data Validity

### Context
Check constraints allow you to enforce arbitrary logic on a row.

### Tasks

#### Task 1.1: The Price Floor
Create a table `products_checked` with `price NUMERIC`.
Add a check constraint that ensures `price` is always positive (> 0).

#### Task 1.2: Valid Status
Create a table `jobs` with `status TEXT`.
Add a constraint ensuring status is one of: 'Pending', 'Running', 'Done', 'Failed'.

---

## Deliverables

For each exercise, provide:
1. SQL Query
2. Attempt to violate constraint and show error
