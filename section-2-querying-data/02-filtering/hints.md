# Hints: Filtering Data

## Exercise 1 Hints

### Task 1.1: Comparison Operators

<details>
<summary>Hint 1: Exact equality</summary>

Use `=` for exact matches. For prices: `WHERE price = 49.99`
</details>

<details>
<summary>Hint 2: Date comparisons</summary>

Dates can be compared with `<`, `>`, `<=`, `>=`. Format dates as strings: `'2025-01-01'`

PostgreSQL automatically understands ISO date format (YYYY-MM-DD).
</details>

<details>
<summary>Hint 3: Not equal</summary>

You can use `!=` or `<>` for "not equal". Both work the same in PostgreSQL.
</details>

### Task 1.2: Boolean Filtering

<details>
<summary>Hint 1: Boolean shorthand</summary>

For boolean columns, `WHERE is_active` is equivalent to `WHERE is_active = true`.

But what about NULL values? A NULL boolean is neither true nor false...
</details>

<details>
<summary>Hint 2: The difference</summary>

If `is_active` could be NULL:
- `WHERE is_active = true` returns only TRUE rows
- `WHERE is_active` returns only TRUE rows
- `WHERE is_active IS NOT FALSE` returns TRUE and NULL rows

The difference matters when NULLs exist.
</details>

### Task 1.3: Date Filtering

<details>
<summary>Hint 1: Month filtering</summary>

To find dates in January 2025, you need a range:
`WHERE last_restocked >= '2025-01-01' AND last_restocked < '2025-02-01'`

Or use EXTRACT: `WHERE EXTRACT(MONTH FROM last_restocked) = 1 AND EXTRACT(YEAR FROM last_restocked) = 2025`

Which approach is better for performance?
</details>

<details>
<summary>Hint 2: Days ago</summary>

`CURRENT_DATE` gives today's date. You can subtract intervals:
`CURRENT_DATE - INTERVAL '30 days'` or `CURRENT_DATE - 30`
</details>

<details>
<summary>Hint 3: Never restocked</summary>

"Never restocked" means the column is NULL. Use `IS NULL`, not `= NULL`.
</details>

---

## Exercise 2 Hints

### Task 2.1 & 2.2: AND/OR

<details>
<summary>Hint 1: Combining with AND</summary>

All conditions must be true. Simply chain them:
`WHERE condition1 AND condition2 AND condition3`
</details>

<details>
<summary>Hint 2: Combining with OR</summary>

Any condition being true includes the row:
`WHERE condition1 OR condition2 OR condition3`
</details>

### Task 2.3: Precedence

<details>
<summary>Hint 1: AND vs OR precedence</summary>

AND has higher precedence than OR. So:
`WHERE A OR B AND C` 

Is evaluated as:
`WHERE A OR (B AND C)`

NOT as:
`WHERE (A OR B) AND C`
</details>

<details>
<summary>Hint 2: Use parentheses</summary>

Always use parentheses to make your intent clear:
`WHERE (condition1 OR condition2) AND condition3`

This removes ambiguity and makes code more readable.
</details>

### Task 2.4: Complex Conditions

<details>
<summary>Hint</summary>

Break it down:
1. First, define "Electronics accessories": `category = 'Electronics' AND subcategory = 'Accessories'`
2. Then "Furniture storage": `category = 'Furniture' AND subcategory = 'Storage'`
3. Combine with OR, wrap in parentheses
4. Then AND with other conditions
</details>

---

## Exercise 3 Hints

### Task 3.1: BETWEEN

<details>
<summary>Hint 1: BETWEEN is inclusive</summary>

`BETWEEN 10 AND 50` includes both 10 and 50.

To prove it: `SELECT 10 BETWEEN 10 AND 50` returns TRUE.
</details>

<details>
<summary>Hint 2: Date BETWEEN</summary>

Be careful with timestamps! `BETWEEN '2025-01-10' AND '2025-01-20'` might miss data from January 20th if there's a time component.

For DATE columns it's fine. For TIMESTAMP, consider using `< '2025-01-21'` for the upper bound.
</details>

### Task 3.2: IN

<details>
<summary>Hint</summary>

`IN` is shorthand for multiple OR conditions:
`WHERE category IN ('A', 'B')` equals `WHERE category = 'A' OR category = 'B'`
</details>

### Task 3.3: NOT IN with NULL

<details>
<summary>Hint 1: The NULL trap</summary>

`WHERE x NOT IN (1, 2, NULL)` returns NO ROWS!

Why? `x NOT IN (1, 2, NULL)` expands to:
`x != 1 AND x != 2 AND x != NULL`

And `x != NULL` is UNKNOWN (not TRUE), making the whole expression UNKNOWN.
</details>

<details>
<summary>Hint 2: Avoiding the trap</summary>

Either ensure no NULLs in your list, or use NOT EXISTS instead:
```sql
WHERE NOT EXISTS (
  SELECT 1 FROM values_table WHERE values_table.value = main_table.x
)
```
</details>

---

## Exercise 4 Hints

### Task 4.1: Scalar Subqueries

<details>
<summary>Hint 1: Average in subquery</summary>

```sql
WHERE price > (SELECT AVG(price) FROM products)
```

The subquery must return exactly ONE value (one row, one column) to be used with `>`, `<`, `=`.
</details>

### Task 4.2: IN with Subqueries

<details>
<summary>Hint 1: Categories with inactive products</summary>

First, what categories have inactive products?
`SELECT category FROM products WHERE is_active = false`

Then use this as a subquery in IN:
`WHERE category IN (SELECT category FROM ... )`
</details>

### Task 4.3: EXISTS

<details>
<summary>Hint 1: EXISTS syntax</summary>

```sql
WHERE EXISTS (
  SELECT 1 
  FROM other_table 
  WHERE other_table.key = main_table.key
)
```

EXISTS returns TRUE if the subquery returns ANY rows. It doesn't matter what columns you select.
</details>

<details>
<summary>Hint 2: EXISTS vs IN performance</summary>

- IN: The subquery runs once, then all results are compared
- EXISTS: The subquery can stop as soon as it finds one match

For large subquery results, EXISTS often performs better because it can "short-circuit".

EXISTS also handles NULLs better than IN.
</details>

---

## Exercise 5 Hints

### Task 5.2: Case Sensitivity

<details>
<summary>Hint 1: Case comparison</summary>

PostgreSQL string comparisons are case-sensitive by default.
'Electronics' != 'electronics'
</details>

<details>
<summary>Hint 2: Case-insensitive options</summary>

1. `WHERE LOWER(category) = 'electronics'` - converts to lowercase
2. `WHERE category ILIKE 'electronics'` - case-insensitive LIKE
3. `WHERE category ~* 'electronics'` - case-insensitive regex

Option 1 is most portable. Option 2 is PostgreSQL-specific but clear.
</details>

<details>
<summary>Hint 3: Performance implication</summary>

`WHERE LOWER(category) = 'electronics'` can't use a regular index on `category`.

You'd need a functional index: `CREATE INDEX ON products (LOWER(category))`
</details>

### Task 5.3: Numeric Precision

<details>
<summary>Hint: Floating point comparison</summary>

Due to binary representation, 49.99 might be stored as 49.98999999999... in REAL/FLOAT.

Safe comparison: `WHERE ABS(price - 49.99) < 0.001`

Or: Use DECIMAL/NUMERIC for money (which this table does).
</details>

---

## Exercise 6 Hints

### Challenge 6.1: Inventory Alert System

<details>
<summary>Hint</summary>

Use CASE WHEN with your conditions:
```sql
SELECT 
  name,
  CASE 
    WHEN stock_quantity = 0 AND is_active THEN 'CRITICAL'
    WHEN stock_quantity <= reorder_level AND is_active THEN 'WARNING'
    -- ... more conditions
    ELSE 'OK'
  END AS alert_level
FROM products
```

Order matters! CASE evaluates top-to-bottom and stops at first match.
</details>

### Challenge 6.2: Dynamic Pricing

<details>
<summary>Hint</summary>

First calculate margin: `(price - cost) / price * 100`

Then use CASE to categorize. You might also want to define what "low stock" and "high stock" mean for your recommendation.
</details>

### Challenge 6.3: Data Quality Audit

<details>
<summary>Hint 1: Finding issues</summary>

You need a WHERE clause with OR to find rows with ANY issue:
`WHERE description IS NULL OR sku IS NULL OR ...`
</details>

<details>
<summary>Hint 2: Showing which issues</summary>

Use CASE or string concatenation to build an "issues" column:
```sql
CASE WHEN description IS NULL THEN 'Missing description; ' ELSE '' END ||
CASE WHEN sku IS NULL THEN 'Missing SKU; ' ELSE '' END ||
-- ... more
AS issues
```
</details>

---

## General Tips

1. **Build incrementally**: Start with one condition, verify it works, then add more.

2. **Test boundaries**: When using `<`, `<=`, `BETWEEN`, verify the boundary cases.

3. **Watch for NULLs**: Conditions involving columns that can be NULL often need special handling.

4. **Use parentheses liberally**: They clarify intent and prevent precedence bugs.

5. **Consider what should NOT match**: Sometimes it's easier to think about exclusions.
