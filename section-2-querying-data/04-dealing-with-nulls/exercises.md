# Exercise: Dealing with NULLs

## Prerequisites
- Completed previous exercises
- Understanding of filtering and pattern matching
- The `products` table with all previously inserted data

## Additional Setup

Add products with strategic NULL values:

```sql
INSERT INTO products (name, category, subcategory, price, cost, stock_quantity, reorder_level, supplier_id, weight_kg, is_active, last_restocked, description, sku) VALUES
('Mystery Box', 'Office Supplies', NULL, 19.99, NULL, 25, 10, NULL, NULL, true, NULL, 'Surprise office supplies box', 'OFSP-MB-001'),
('Clearance Item A', NULL, NULL, 5.99, 2.00, 50, NULL, 5, 0.100, NULL, '2024-01-15', NULL, 'CLEA-CI-001'),
('Prototype Widget', 'Electronics', 'Experimental', NULL, NULL, 0, 0, NULL, NULL, false, NULL, 'Prototype - not for sale', NULL),
('Refurbished Monitor', 'Electronics', 'Displays', 149.99, NULL, 3, 1, 1, NULL, true, NULL, 'Factory refurbished 24" monitor', 'ELEC-RM-001');
```

---

## Exercise 1: Understanding NULL

### Context
NULL in SQL means "unknown" or "missing value." It's NOT the same as zero, empty string, or false. NULL comparisons follow three-valued logic (TRUE, FALSE, UNKNOWN), which catches many developers off guard.

### Tasks

#### Task 1.1: NULL Basics
Predict the result of each query BEFORE running it, then verify:

```sql
-- Query 1
SELECT NULL = NULL;

-- Query 2  
SELECT NULL != NULL;

-- Query 3
SELECT NULL > 0;

-- Query 4
SELECT 1 + NULL;

-- Query 5
SELECT 'hello' || NULL;

-- Query 6
SELECT NULL AND TRUE;

-- Query 7
SELECT NULL OR TRUE;

-- Query 8
SELECT NOT NULL;
```

For each, explain WHY the result is what it is.

#### Task 1.2: NULL in WHERE Clauses
Write queries to find:
1. All products with NULL subcategory
2. All products where cost is NOT NULL
3. All products where EITHER category OR subcategory is NULL
4. All products where BOTH category AND cost are NULL

#### Task 1.3: NULL Comparison Trap
Explain what's wrong with these queries and fix them:

```sql
-- Intended: Find products with no supplier
SELECT * FROM products WHERE supplier_id = NULL;

-- Intended: Find products that have different cost and price
SELECT * FROM products WHERE cost != price;

-- Intended: Find products not in Electronics
SELECT * FROM products WHERE category != 'Electronics';
```

---

## Exercise 2: IS NULL and IS NOT NULL

### Context
The only way to reliably test for NULL is using `IS NULL` and `IS NOT NULL`. These are special predicates, not comparison operators.

### Tasks

#### Task 2.1: Basic NULL Detection
1. Find all products with missing (NULL) descriptions
2. Find all products with missing cost information
3. Find products that have NEVER been restocked (NULL last_restocked)
4. Find products with complete data (no NULL values in any column except description, which can be optional)

#### Task 2.2: NULL Counts
Write queries to count:
1. How many products have NULL category?
2. How many products have NULL cost?
3. What percentage of products have NULL supplier_id?
4. Which columns have the most NULLs? (Show column name and NULL count)

---

## Exercise 3: COALESCE

### Context
COALESCE returns the first non-NULL value from a list of arguments. It's essential for providing default values and handling missing data in calculations and displays.

### Tasks

#### Task 3.1: Default Values
1. Display all products with their cost. Show "TBD" for products with NULL cost.
2. Show supplier_id, displaying "Unknown" when NULL
3. Show weight_kg, displaying "0.000" when NULL (as a number, not text)

#### Task 3.2: Fallback Chains
1. Display a "display name" for each product that uses: `description` if available, otherwise `name`
2. Create a "full classification" showing: `subcategory` if available, otherwise `category` if available, otherwise "Uncategorized"
3. Calculate profit margin, treating NULL cost as 0 (what's the problem with this approach?)

#### Task 3.3: COALESCE in Calculations
1. Calculate total inventory value: `price * stock_quantity`. Handle NULL prices by using cost * 1.5 as a fallback.
2. Calculate reorder urgency: `stock_quantity / reorder_level`. Use 999 when reorder_level is NULL to indicate "no reorder threshold".
3. Show days since last restock, with "Never restocked" for NULL dates

---

## Exercise 4: NULLIF

### Context
NULLIF returns NULL if two arguments are equal; otherwise returns the first argument. It's the inverse of COALESCE and is crucial for preventing division by zero and handling sentinel values.

### Tasks

#### Task 4.1: Division by Zero Prevention
1. Calculate `stock_quantity / reorder_level` safely for all products
2. Calculate the price-to-cost ratio, handling cases where cost is 0 or NULL
3. Show how many times current stock covers the reorder level, safely handling all edge cases

#### Task 4.2: Sentinel Value Handling
Imagine some systems use 0 to mean "unknown" instead of NULL.

1. Write a query that treats reorder_level of 0 as if it were NULL when displaying
2. Show weight_kg, treating 0 as "Not measured" (as if it were NULL)
3. Calculate average cost, excluding both NULL and 0 values

#### Task 4.3: NULLIF vs CASE
Rewrite these NULLIF expressions using CASE WHEN, and vice versa:

```sql
-- Convert to CASE:
SELECT NULLIF(reorder_level, 0) FROM products;

-- Convert to NULLIF:
SELECT CASE WHEN category = 'Unknown' THEN NULL ELSE category END FROM products;
```

Which is more readable? When would you choose one over the other?

---

## Exercise 5: NULL and Aggregates

### Context
Aggregate functions handle NULL differently than you might expect. Understanding this behavior is crucial for accurate reporting.

### Tasks

#### Task 5.1: Aggregate Behavior
For each aggregate, show the result and explain NULL handling:
1. `SELECT COUNT(*), COUNT(cost), COUNT(supplier_id) FROM products;`
2. `SELECT AVG(cost), SUM(cost), SUM(cost)/COUNT(*) FROM products;`
3. `SELECT MIN(last_restocked), MAX(last_restocked) FROM products;`

Why might `AVG(cost)` differ from `SUM(cost)/COUNT(*)`?

#### Task 5.2: Intentional NULL Inclusion
1. Calculate the TRUE average cost, treating NULL as 0
2. Calculate what percentage of products have unknown (NULL) cost
3. Show the difference between "average cost of products with known cost" vs "average cost treating unknowns as 0"

#### Task 5.3: GROUP BY with NULL
1. Group products by category and count them. What happens to NULLs?
2. Group products by subcategory. How are NULL subcategories displayed?
3. Modify the query to show "No Subcategory" instead of NULL in the results

---

## Exercise 6: NULL in DISTINCT and UNION

### Context
NULL has special behavior in set operations and distinct counting.

### Tasks

#### Task 6.1: DISTINCT and NULL
1. `SELECT DISTINCT subcategory FROM products;` - How many rows? How is NULL treated?
2. `SELECT DISTINCT category, subcategory FROM products;` - Can there be multiple rows with NULL subcategory?

#### Task 6.2: UNION and NULL
Consider these tables (create them temporarily):

```sql
CREATE TEMP TABLE set_a (val INTEGER);
CREATE TEMP TABLE set_b (val INTEGER);
INSERT INTO set_a VALUES (1), (2), (NULL);
INSERT INTO set_b VALUES (2), (3), (NULL);
```

1. What does `SELECT * FROM set_a UNION SELECT * FROM set_b` return?
2. What does `SELECT * FROM set_a INTERSECT SELECT * FROM set_b` return?
3. What does `SELECT * FROM set_a EXCEPT SELECT * FROM set_b` return?

Explain how NULL is treated in each set operation.

---

## Exercise 7: Comprehensive NULL Challenges

### Challenge 7.1: Data Quality Report
Create a comprehensive data quality report showing:
- Product name
- A "completeness score" (percentage of non-NULL columns out of all columns)
- A list of which columns are NULL for each product
- Flag products with less than 70% completeness

### Challenge 7.2: Safe Calculation Engine
Write a single query that shows for each product:
- Name
- Price (or "Price TBD" if NULL)
- Cost (or "Cost TBD" if NULL)
- Profit (price - cost), handling all NULL scenarios:
  - If both NULL: "Cannot calculate"
  - If only price NULL: "Need price"
  - If only cost NULL: "Need cost"  
  - If both present: Show the actual profit
- Profit margin percentage with same NULL handling

### Challenge 7.3: Business Logic with NULLs
A business rule states:
- Products are "orderable" if: is_active = true AND stock_quantity > 0 AND price IS NOT NULL
- Products need "review" if: is_active IS NULL OR (is_active = true AND cost IS NULL)
- Products are "archived" if: is_active = false

Write a query that categorizes ALL products into exactly one category. Handle the edge cases where multiple conditions might match or none match.

---

## Deliverables

For each exercise, provide:
1. The SQL query
2. Explanation of NULL handling logic
3. Edge cases discovered
4. Any "gotchas" that surprised you

**Evaluation Criteria**:
- Correct understanding of three-valued logic
- Appropriate use of IS NULL vs = NULL
- Proper use of COALESCE and NULLIF
- Awareness of aggregate NULL behavior
