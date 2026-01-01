# Exercise: Filtering Data

## Prerequisites
- Completed "Exploring the Data" exercises
- Understanding of SELECT, ORDER BY, LIMIT
- The `products` table from the previous exercise

## Additional Setup

Add more data for richer filtering exercises:

```sql
INSERT INTO products (name, category, subcategory, price, cost, stock_quantity, reorder_level, supplier_id, weight_kg, is_active, last_restocked, description, sku) VALUES
('Bluetooth Headphones', 'Electronics', 'Audio', 79.99, 35.00, 45, 15, 1, 0.250, true, '2025-01-17', 'Over-ear Bluetooth headphones with ANC', 'ELEC-BH-001'),
('USB Flash Drive 64GB', 'Electronics', 'Storage', 12.99, 5.00, 500, 100, 2, 0.015, true, '2025-01-20', '64GB USB 3.0 flash drive', 'ELEC-FD-001'),
('Whiteboard Markers', 'Office Supplies', 'Writing', 8.99, 3.00, 200, 50, 5, 0.150, true, '2025-01-15', 'Set of 8 dry erase markers', 'OFSP-WM-001'),
('File Cabinet', 'Furniture', 'Storage', 149.99, 70.00, 5, 2, 4, 25.000, true, '2024-10-15', '3-drawer metal file cabinet', 'FURN-FC-001'),
('Paper Shredder', 'Office Supplies', 'Equipment', 89.99, 42.00, 15, 5, 5, 6.500, false, '2024-09-01', 'Cross-cut paper shredder, 10 sheets', 'OFSP-PS-001'),
('Desk Mat', 'Office Supplies', 'Desk Accessories', 19.99, 8.00, 75, 20, 5, 0.600, true, '2025-01-10', 'Large leather desk mat, 90x40cm', 'OFSP-DM-001'),
('HDMI Cable 2m', 'Electronics', 'Cables', 9.99, 3.50, 300, 75, 2, 0.100, true, '2025-01-22', 'HDMI 2.1 cable, 2 meters', 'ELEC-HC-001'),
('Bookshelf', 'Furniture', 'Storage', 129.99, 55.00, 3, 2, 4, 20.000, true, '2024-08-20', '5-tier wooden bookshelf', 'FURN-BS-001'),
('Wireless Earbuds', 'Electronics', 'Audio', 49.99, 20.00, 120, 30, 1, 0.050, true, '2025-01-19', 'True wireless earbuds with charging case', 'ELEC-WE-001'),
('Stapler', 'Office Supplies', 'Tools', 6.99, 2.50, 180, 40, 5, 0.250, true, '2025-01-08', 'Heavy-duty stapler, 50 sheet capacity', 'OFSP-ST-001');
```

---

## Exercise 1: Basic WHERE Clauses

### Context
The WHERE clause is your primary tool for filtering data. Understanding comparison operators and their behavior with different data types is essential.

### Tasks

#### Task 1.1: Comparison Operators
Write queries to find:
1. All products priced at exactly $49.99
2. All products priced under $20
3. All products with stock quantity of 100 or more
4. All products that are NOT in the 'Electronics' category
5. All products that were last restocked on or after January 1st, 2025

#### Task 1.2: Boolean Filtering
1. Find all inactive products
2. Find all active products (write this TWO different ways)
3. Explain: What's the difference between `WHERE is_active = true` and `WHERE is_active`? When might they produce different results?

#### Task 1.3: Date Filtering
1. Find products restocked in January 2025
2. Find products restocked more than 30 days ago (from current date)
3. Find products that have NEVER been restocked

---

## Exercise 2: Combining Conditions

### Context
Real-world queries almost always require multiple conditions. Understanding AND, OR, and their precedence is critical for writing correct queries.

### Tasks

#### Task 2.1: AND Conditions
Find all products that meet ALL of these criteria:
- Category is 'Electronics'
- Price is between $20 and $60 (inclusive)
- Currently in stock (stock_quantity > 0)
- Active

#### Task 2.2: OR Conditions
Find all products that meet ANY of these criteria:
- Stock is 0 (out of stock)
- Stock is at or below reorder level
- Product is inactive

#### Task 2.3: Precedence Challenge
Consider this business rule: "Flag products that need attention: either (Electronics with low stock) OR (any inactive product with stock remaining)"

1. Write this query correctly
2. Now write an INCORRECT version that looks similar but produces wrong results due to AND/OR precedence
3. Explain the difference

#### Task 2.4: Complex Conditions
Find products that match this criteria:
- (Electronics accessories OR Furniture storage items) 
- AND price under $50
- AND currently active
- AND have been restocked in 2025

---

## Exercise 3: BETWEEN and IN

### Context
BETWEEN and IN are syntactic shortcuts that make queries more readable. Understanding their exact behavior (inclusive vs exclusive, NULL handling) is important.

### Tasks

#### Task 3.1: BETWEEN
1. Find products priced between $10 and $50
2. Find products restocked between January 10, 2025 and January 20, 2025
3. **Critical Question**: Is BETWEEN inclusive or exclusive on its boundaries? Write a query to prove your answer.

#### Task 3.2: IN
1. Find products in these categories: 'Electronics', 'Furniture'
2. Find products supplied by suppliers 1, 2, or 5
3. Find products with stock quantities of exactly 0, 45, 75, or 120

#### Task 3.3: NOT BETWEEN and NOT IN
1. Find products NOT priced between $20 and $100
2. Find products NOT in 'Office Supplies' or 'Furniture' categories
3. **Challenge**: What happens with `NOT IN` if the list contains NULL? Test with: `WHERE supplier_id NOT IN (1, 2, NULL)`. Explain the result.

---

## Exercise 4: Subqueries in WHERE

### Context
Sometimes you need to filter based on values from another query. Subqueries in WHERE clauses enable dynamic filtering.

### Tasks

#### Task 4.1: Scalar Subqueries
1. Find all products priced above the average price
2. Find all products with stock below the average stock level
3. Find products that cost more than the cheapest Electronics item's price

#### Task 4.2: IN with Subqueries
1. Find all products in categories that have at least one inactive product
2. Find all products from suppliers who supply items over $100
3. Find products whose subcategory appears in more than one category

#### Task 4.3: EXISTS Subqueries
1. Rewrite Task 4.2.1 using EXISTS instead of IN
2. **Critical Question**: When would you prefer EXISTS over IN? (Consider performance with large datasets)

---

## Exercise 5: Filtering Edge Cases

### Context
Edge cases often cause bugs in production. These exercises test your understanding of tricky filtering scenarios.

### Tasks

#### Task 5.1: Empty Results
Write queries that return no results based on the current data, and explain why:
1. Products in a category that doesn't exist
2. Products with negative profit (price < cost)
3. Active products with NULL last_restocked date that are in 'Electronics'

#### Task 5.2: Case Sensitivity
1. Test: Does `WHERE category = 'electronics'` return the same results as `WHERE category = 'Electronics'`?
2. Write a case-insensitive search for category 'electronics'
3. What are the performance implications of case-insensitive filtering?

#### Task 5.3: Numeric Precision
1. Find products where price equals exactly 49.99
2. **Challenge**: If price were stored as REAL instead of DECIMAL, demonstrate why `WHERE price = 49.99` might not work as expected
3. How would you safely compare floating-point numbers?

---

## Exercise 6: Business Scenario Challenges

### Context
Apply your filtering knowledge to real business questions.

### Tasks

#### Challenge 6.1: Inventory Alert System
Create a query that categorizes products into alert levels:
- **CRITICAL**: Out of stock (stock = 0) AND active
- **WARNING**: At or below reorder level AND active
- **REVIEW**: Inactive but still has stock
- **OK**: Everything else

Show product name, category, stock, reorder level, is_active, and the alert level.

#### Challenge 6.2: Dynamic Pricing Candidates
Find products that might be candidates for price adjustment:
- High margin items (profit margin > 50%) with low stock (could increase price)
- Low margin items (profit margin < 30%) with high stock (might need discount)

Show product name, current price, cost, margin percentage, stock, and a recommendation column.

#### Challenge 6.3: Data Quality Audit
Write a comprehensive query to find ALL products with potential data quality issues:
- Missing description
- No SKU
- Never restocked but active
- Price lower than cost
- Zero or negative reorder level
- Weight seems unreasonable (> 50kg or = 0)

Each row should show the product name and which specific issue(s) it has.

---

## Deliverables

For each exercise, provide:
1. The complete SQL query
2. The number of rows returned
3. Explanation of why certain rows are included/excluded
4. Any edge cases you discovered

**Evaluation Criteria**:
- Correct use of comparison operators
- Proper handling of AND/OR precedence
- Understanding of NULL behavior in filters
- Ability to translate business requirements into WHERE clauses
