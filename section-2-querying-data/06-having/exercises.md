# Exercise: Having

## Prerequisites
- Completed "Aggregating Data" exercises
- The `sales` table from the previous exercise

## Additional Setup
None required if `sales` table exists.

---

## Exercise 1: The Difference Between WHERE and HAVING

### Context
This is the most common confusion for SQL beginners.
- `WHERE` filters rows **before** aggregation.
- `HAVING` filters groups **after** aggregation.

### Tasks

#### Task 1.1: Filtering Before vs After
1. Write a query to show the total sales quantity for product_id 1. (Use WHERE)
2. Write a query to show the total sales quantity for EACH product, but ONLY display products that have sold more than 10 units in total. (Use HAVING)
3. **Conceptual**: Explain why you cannot use `WHERE sum(quantity) > 10`?

#### Task 1.2: Combining WHERE and HAVING
1. Calculate the total revenue per region, but only for sales made in 2025.
2. Filter the result of step 1 to show only regions with total revenue > $500.
3. Identify which part of the query handled the date filter and which part handled the revenue filter.

---

## Exercise 2: Basic HAVING Conditions

### Context
Using comparison operators on aggregate results.

### Tasks

#### Task 2.1: Revenue Thresholds
1. Find all regions that have generated more than $1000 in total revenue.
2. Find all products that have an *average* selling price higher than $50.

#### Task 2.2: Count Thresholds
1. Find dates where more than 3 distinct sales transactions occurred.
2. Find products that have been sold in more than 1 region.

---

## Exercise 3: Complex HAVING Conditions

### Context
You can use complex logic inside HAVING, just like in WHERE.

### Tasks

#### Task 3.1: Logical Operators
1. Find regions that have EITHER > 100 items sold OR > $1000 revenue.
2. Find products with total sales between $100 and $500.

#### Task 3.2: Aggregates in HAVING only
1. Find regions where the *average* unit price is greater than 50, but don't include the average price in the SELECT list (just select the region).
2. Is this valid? Why or why not?

---

## Exercise 4: Challenge Problems

### Challenge 4.1: High Value Days
Find days where the total revenue exceeded $200 AND at least 2 different products were sold.

### Challenge 4.2: Consistent Performers
Find products that have been sold on at least 3 different days AND have a total quantity sold greater than 20.

### Challenge 4.3: The "Average" Region
Find regions where the average sale amount (revenue per transaction) is lower than the global average sale amount across all regions.
*Hint: You might need a subquery inside the HAVING clause.*

---

## Deliverables

For each exercise, provide:
1. The SQL query
2. Explanation of why WHERE or HAVING was chosen
3. Sample output

**Evaluation Criteria**:
- Correct distinction between row-level filtering (WHERE) and group-level filtering (HAVING)
- Ability to combine both in a single query
- Using aggregates in HAVING that are not present in SELECT (valid SQL behavior)
