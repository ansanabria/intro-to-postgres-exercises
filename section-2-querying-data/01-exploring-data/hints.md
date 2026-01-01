# Hints: Exploring the Data

## Exercise 1 Hints

### Task 1.1: Schema Exploration

<details>
<summary>Hint 1: Where is schema information stored?</summary>

PostgreSQL stores metadata about all database objects in special system tables. The `information_schema` is a standardized way to access this information. Look for a view called `information_schema.columns`.
</details>

<details>
<summary>Hint 2: Finding constraints</summary>

Constraints are stored in `information_schema.table_constraints` and `information_schema.constraint_column_usage`. You can also use `\d tablename` in psql or look at `pg_constraint` system catalog.
</details>

### Task 1.2: Data Sampling

<details>
<summary>Hint 1: Random ordering</summary>

PostgreSQL has a function that returns a random number between 0 and 1. If you ORDER BY this function, what happens to your rows?
</details>

<details>
<summary>Hint 2: Pagination</summary>

`LIMIT` controls how many rows to return. `OFFSET` controls how many rows to skip. But what happens when you `OFFSET 10000` on a 10001 row table?
</details>

<details>
<summary>Hint 3: OFFSET Performance Problem</summary>

With `OFFSET`, the database still has to read and discard all the skipped rows. For page 1000 with 10 items per page, that's 10,000 rows read just to show 10. 

Alternative: "Keyset pagination" - instead of "skip 10000 rows", say "get rows WHERE id > last_seen_id LIMIT 10".
</details>

---

## Exercise 2 Hints

### Task 2.1: Selective Retrieval

<details>
<summary>Hint 1: Concatenating strings</summary>

The `||` operator concatenates strings in PostgreSQL. You can also use the `CONCAT()` function. Which handles NULL values differently?
</details>

<details>
<summary>Hint 2: Formatting currency</summary>

You can concatenate a '$' symbol with your price. But how do you ensure the price shows exactly 2 decimal places? Look into `TO_CHAR()` or `ROUND()`.
</details>

<details>
<summary>Hint 3: Calculated columns</summary>

You can do arithmetic in SELECT: `price - cost AS profit`. Remember to alias calculated columns for clarity.
</details>

### Task 2.2: Data Type Awareness

<details>
<summary>Hint 1: Type incompatibility</summary>

What happens if you try to concatenate a string with a number directly? Try: `SELECT 'Price: ' || price FROM products`
</details>

<details>
<summary>Hint 2: Casting</summary>

Use `CAST(value AS type)` or `value::type` to convert between types. For example, `price::TEXT` converts price to text.
</details>

<details>
<summary>Hint 3: Decimal precision</summary>

INTEGER division truncates: `5 / 2 = 2`. DECIMAL/NUMERIC preserves precision. REAL/FLOAT can have floating-point representation issues. For money and percentages, which is safest?
</details>

---

## Exercise 3 Hints

### Task 3.1: Complex Ordering

<details>
<summary>Hint 1: Multiple ORDER BY columns</summary>

You can order by multiple columns separated by commas. Each can have its own ASC/DESC.
</details>

<details>
<summary>Hint 2: Ordering booleans</summary>

In PostgreSQL, FALSE < TRUE. So `ORDER BY is_active` puts inactive first. To get active first, what would you do?
</details>

### Task 3.2: NULL Ordering

<details>
<summary>Hint 1: NULLS FIRST/LAST</summary>

PostgreSQL has explicit syntax for NULL ordering: `ORDER BY column NULLS FIRST` or `ORDER BY column NULLS LAST`.
</details>

<details>
<summary>Hint 2: Default behavior</summary>

By default, PostgreSQL treats NULLs as "larger than" any other value. So in ASC order, NULLs appear... where? In DESC order?
</details>

### Task 3.3: Finding Extremes

<details>
<summary>Hint 1: Single extreme value</summary>

If you ORDER BY the column you want the extreme of and LIMIT 1, you get the extreme value without needing MIN/MAX.
</details>

<details>
<summary>Hint 2: Calculated extremes</summary>

You can ORDER BY calculated expressions, not just column names. The profit margin is a calculation - can you ORDER BY it?
</details>

---

## Exercise 4 Hints

### Task 4.1: Unique Values

<details>
<summary>Hint 1: DISTINCT on single column</summary>

`SELECT DISTINCT column FROM table` gives unique values of that column.
</details>

<details>
<summary>Hint 2: DISTINCT on multiple columns</summary>

`SELECT DISTINCT col1, col2 FROM table` gives unique COMBINATIONS. A row is only a duplicate if BOTH columns match.
</details>

<details>
<summary>Hint 3: Counting distinct values</summary>

You can use `COUNT(DISTINCT column)` to count unique values instead of listing them.
</details>

### Task 4.2: DISTINCT ON

<details>
<summary>Hint 1: DISTINCT ON syntax</summary>

`SELECT DISTINCT ON (column) * FROM table ORDER BY column, other_column`

The columns in DISTINCT ON must be the leftmost columns in ORDER BY. The second ORDER BY column determines WHICH row is kept.
</details>

<details>
<summary>Hint 2: Getting the most expensive per category</summary>

If you DISTINCT ON (category) and ORDER BY category, price DESC, you'll get one row per category - the one with the highest price in each.
</details>

<details>
<summary>Hint 3: DISTINCT ON vs GROUP BY</summary>

GROUP BY requires aggregation - you must tell it what to do with non-grouped columns (SUM, MAX, etc.). 

DISTINCT ON lets you keep ALL columns of a specific row without aggregation - you're selecting entire rows, not computing summaries.
</details>

---

## Exercise 5 Hints

### Inventory Value Report

<details>
<summary>Hint</summary>

Calculate in SELECT, filter with WHERE, order with ORDER BY. The condition `> 500` goes in WHERE, not HAVING (no GROUP BY here).
</details>

### Reorder Alert

<details>
<summary>Hint</summary>

The condition is `stock_quantity <= reorder_level`. 

For "how many below": `reorder_level - stock_quantity`. But this could be negative if stock > reorder. Use `GREATEST(expression, 0)` to ensure minimum of 0.
</details>

### Profitability Analysis

<details>
<summary>Hint</summary>

Multiple conditions in WHERE: `WHERE is_active = true AND stock_quantity > 0`

For rounding: `ROUND(expression, 2)`

Remember: `LIMIT` with `ORDER BY DESC` gets the "top N".
</details>

### Data Quality Check

<details>
<summary>Hint</summary>

This is asking for rows that match ANY of several conditions - use OR to combine them.

But showing "which issue" is trickier. Consider using `CASE WHEN` to create a column that indicates the type of issue found.

Alternatively, you could UNION multiple queries, each finding one type of issue.
</details>

---

## General Tips

1. **Test incrementally**: Start with `SELECT *` to see the data, then refine your columns and conditions.

2. **Use table aliases**: For readability, especially with longer queries: `FROM products p`

3. **Comment your queries**: Use `--` for single-line comments to explain complex logic.

4. **Check for NULLs**: Many exercises have NULL values. Make sure your query handles them appropriately.
