# Exercise: Generated Columns from JSON

## Prerequisites
- Completed "Accessing JSONB Data"

---

## Exercise 1: Extracting to Column

### Context
If you query a JSON field frequently, it's efficient to materialize it into a generated column.

### Tasks

#### Task 1.1: The Customer Email
Alter the `orders` table to add a GENERATED ALWAYS column `email` extracted from `customer_info->>'email'`.

#### Task 1.2: Querying
Write a query to find orders by email using the new column. Verify that you don't need to touch the JSON blob in the WHERE clause.

---

## Exercise 2: Indexing Generated Columns

### Context
You can index the generated column just like a regular column.

### Tasks

#### Task 2.1: The Optimization
Create an index on the generated `email` column.
Explain why this might be better than a functional index on the JSON field.

---

## Deliverables

For each exercise, provide:
1. SQL Query
2. Explanation of benefits
