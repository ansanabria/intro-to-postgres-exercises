# Hints: Dealing with NULLs

## Exercise 1 Hints

### Task 1.1: NULL Basics

<details>
<summary>Hint 1: NULL = NULL</summary>

NULL means "unknown". Is an unknown value equal to another unknown value? We can't know! So `NULL = NULL` returns `NULL` (unknown), not `TRUE`.
</details>

<details>
<summary>Hint 2: NULL in arithmetic</summary>

Any arithmetic with NULL returns NULL. If you don't know what X is, you can't know what X + 1 is.
</details>

<details>
<summary>Hint 3: NULL in boolean logic</summary>

Three-valued logic:
- `NULL AND TRUE` = NULL (if the NULL were FALSE, result would be FALSE; if TRUE, result would be TRUE - we don't know)
- `NULL AND FALSE` = FALSE (regardless of NULL, FALSE AND anything = FALSE)
- `NULL OR TRUE` = TRUE (regardless of NULL, TRUE OR anything = TRUE)
- `NULL OR FALSE` = NULL (we don't know what NULL OR FALSE would be)
</details>

### Task 1.2: NULL in WHERE

<details>
<summary>Hint</summary>

Use `IS NULL` and `IS NOT NULL`, not `= NULL` or `!= NULL`.

For OR conditions: `WHERE category IS NULL OR subcategory IS NULL`
For AND conditions: `WHERE category IS NULL AND cost IS NULL`
</details>

### Task 1.3: NULL Comparison Trap

<details>
<summary>Hint 1: Finding NULLs</summary>

`WHERE supplier_id = NULL` returns NO rows because `NULL = NULL` is NULL (unknown), not TRUE. Only TRUE rows pass the filter.

Fix: `WHERE supplier_id IS NULL`
</details>

<details>
<summary>Hint 2: Not equal with NULLs</summary>

`WHERE cost != price` excludes rows where EITHER cost OR price is NULL (because NULL != anything is NULL).

To include NULLs: `WHERE cost != price OR cost IS NULL OR price IS NULL`
Or use `IS DISTINCT FROM`: `WHERE cost IS DISTINCT FROM price`
</details>

<details>
<summary>Hint 3: Not in category</summary>

`WHERE category != 'Electronics'` excludes NULL categories (because NULL != 'Electronics' is NULL).

To include NULL categories: `WHERE category != 'Electronics' OR category IS NULL`
Or: `WHERE category IS DISTINCT FROM 'Electronics'`
</details>

---

## Exercise 2 Hints

### Task 2.1: NULL Detection

<details>
<summary>Hint: Complete data check</summary>

To check multiple columns for NULL, chain with AND:
```sql
WHERE column1 IS NOT NULL 
  AND column2 IS NOT NULL 
  AND column3 IS NOT NULL
  ...
```

Or use: `WHERE COALESCE(col1::text, col2::text, ...) IS NOT NULL` - but this is less clear.
</details>

### Task 2.2: NULL Counts

<details>
<summary>Hint 1: COUNT behavior</summary>

`COUNT(*)` counts all rows.
`COUNT(column)` counts non-NULL values in that column.

So `COUNT(*) - COUNT(column)` gives NULL count.
</details>

<details>
<summary>Hint 2: Percentage calculation</summary>

```sql
SELECT 
  COUNT(*) - COUNT(supplier_id) AS null_count,
  (COUNT(*) - COUNT(supplier_id))::numeric / COUNT(*) * 100 AS null_percentage
FROM products
```
</details>

---

## Exercise 3 Hints

### Task 3.1: Default Values

<details>
<summary>Hint 1: COALESCE basics</summary>

`COALESCE(column, 'default')` returns 'default' if column is NULL.

For numeric defaults: `COALESCE(weight_kg, 0.000)` - note the types must match or be compatible.
</details>

<details>
<summary>Hint 2: Type mismatch</summary>

`COALESCE(cost, 'TBD')` fails because cost is numeric and 'TBD' is text.

Solution: `COALESCE(cost::text, 'TBD')` or use CASE WHEN.
</details>

### Task 3.2: Fallback Chains

<details>
<summary>Hint</summary>

COALESCE takes multiple arguments:
`COALESCE(first_choice, second_choice, third_choice, last_resort)`

It returns the first non-NULL value.
</details>

### Task 3.3: COALESCE in Calculations

<details>
<summary>Hint: Problem with NULL cost as 0</summary>

If cost is NULL and you treat it as 0, your profit margin becomes 100% - misleading!

`(price - COALESCE(cost, 0)) / price * 100` - this shows 100% margin for unknown costs, which is wrong.

Better to show NULL or "Unknown" for such cases.
</details>

---

## Exercise 4 Hints

### Task 4.1: Division by Zero

<details>
<summary>Hint 1: NULLIF for division</summary>

`column / NULLIF(divisor, 0)` returns NULL instead of error when divisor is 0.

`NULLIF(x, 0)` returns NULL if x is 0, otherwise returns x.
</details>

<details>
<summary>Hint 2: Chaining protections</summary>

For both NULL and zero protection:
```sql
stock_quantity / NULLIF(COALESCE(reorder_level, 0), 0)
```

Or more clearly:
```sql
CASE 
  WHEN reorder_level IS NULL OR reorder_level = 0 THEN NULL
  ELSE stock_quantity / reorder_level
END
```
</details>

### Task 4.2: Sentinel Values

<details>
<summary>Hint</summary>

When 0 means "unknown", treat it as NULL:
`NULLIF(column, 0)` converts 0 to NULL.

Then you can use COALESCE for display:
`COALESCE(NULLIF(weight_kg, 0)::text, 'Not measured')`
</details>

### Task 4.3: NULLIF vs CASE

<details>
<summary>Hint</summary>

`NULLIF(x, y)` is exactly equivalent to:
```sql
CASE WHEN x = y THEN NULL ELSE x END
```

NULLIF is more concise for simple equality checks.
CASE is more readable for complex conditions or when you want to return something other than NULL.
</details>

---

## Exercise 5 Hints

### Task 5.1: Aggregate Behavior

<details>
<summary>Hint 1: COUNT variations</summary>

- `COUNT(*)` - counts all rows, regardless of NULLs
- `COUNT(column)` - counts only non-NULL values in that column
- `COUNT(DISTINCT column)` - counts distinct non-NULL values
</details>

<details>
<summary>Hint 2: AVG vs SUM/COUNT</summary>

`AVG(cost)` = `SUM(cost) / COUNT(cost)` - only considers non-NULL values.

`SUM(cost) / COUNT(*)` divides by ALL rows, including those with NULL cost.

These can give very different results!
</details>

### Task 5.2: Including NULLs

<details>
<summary>Hint</summary>

To treat NULL as 0 in average:
`AVG(COALESCE(cost, 0))`

Or: `SUM(COALESCE(cost, 0)) / COUNT(*)`
</details>

### Task 5.3: GROUP BY with NULL

<details>
<summary>Hint</summary>

In GROUP BY, NULLs are grouped together - all NULLs form one group.

To display better:
```sql
SELECT COALESCE(category, 'No Category') AS category, COUNT(*)
FROM products
GROUP BY category  -- or GROUP BY 1
```
</details>

---

## Exercise 6 Hints

### Task 6.1: DISTINCT

<details>
<summary>Hint</summary>

DISTINCT treats all NULLs as equal - you'll only get one NULL row in the result.

For multi-column DISTINCT, (NULL, 'A') and (NULL, 'B') are different rows.
</details>

### Task 6.2: Set Operations

<details>
<summary>Hint</summary>

In UNION, INTERSECT, EXCEPT - NULLs are treated as equal to other NULLs for comparison purposes.

- UNION: Combines sets, removes duplicates (including duplicate NULLs)
- INTERSECT: Returns common values (NULL ∩ NULL = NULL)
- EXCEPT: Returns values in first set not in second
</details>

---

## Exercise 7 Hints

### Challenge 7.1: Completeness Score

<details>
<summary>Hint 1: Counting NULLs per row</summary>

You need to check each column. One approach:
```sql
(CASE WHEN col1 IS NOT NULL THEN 1 ELSE 0 END +
 CASE WHEN col2 IS NOT NULL THEN 1 ELSE 0 END +
 ...) / total_columns::numeric * 100 AS completeness
```
</details>

<details>
<summary>Hint 2: Listing NULL columns</summary>

Build a string:
```sql
CASE WHEN col1 IS NULL THEN 'col1, ' ELSE '' END ||
CASE WHEN col2 IS NULL THEN 'col2, ' ELSE '' END ||
...
```
</details>

### Challenge 7.2: Safe Calculation

<details>
<summary>Hint</summary>

Use nested CASE for complex logic:
```sql
CASE 
  WHEN price IS NULL AND cost IS NULL THEN 'Cannot calculate'
  WHEN price IS NULL THEN 'Need price'
  WHEN cost IS NULL THEN 'Need cost'
  ELSE (price - cost)::text
END AS profit
```
</details>

### Challenge 7.3: Categorization

<details>
<summary>Hint</summary>

Order matters in CASE! Check most specific conditions first:
```sql
CASE
  WHEN is_active = false THEN 'archived'
  WHEN is_active IS NULL OR (is_active = true AND cost IS NULL) THEN 'review'
  WHEN is_active = true AND stock_quantity > 0 AND price IS NOT NULL THEN 'orderable'
  ELSE 'unknown'  -- catch-all for edge cases
END
```
</details>

---

## General Tips

1. **Always ask**: "What happens when this column is NULL?" for every column you use.

2. **Test with NULLs**: Insert test data with strategic NULLs to verify query behavior.

3. **IS DISTINCT FROM**: This operator treats NULLs as equal - `NULL IS NOT DISTINCT FROM NULL` is TRUE.

4. **Document assumptions**: When you use COALESCE to provide defaults, document why that default is appropriate.

5. **Be skeptical of aggregates**: Always check if NULL exclusion affects your results.
