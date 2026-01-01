# Hints: Aggregating Data

## Exercise 1 Hints

### Task 1.1: Simple Counts and Sums

<details>
<summary>Hint 1: Counting</summary>

`COUNT(*)` counts rows. `COUNT(column)` counts non-null values. For "total sales records", `COUNT(*)` is usually what you want.
</details>

<details>
<summary>Hint 2: Revenue Calculation</summary>

You can perform arithmetic inside the aggregate function: `SUM(quantity * unit_price)`.
</details>

### Task 1.2: Averages

<details>
<summary>Hint 1: Average formula</summary>

`AVG(x)` is functionally equivalent to `SUM(x) / COUNT(x)`.
</details>

<details>
<summary>Hint 2: NULL effect</summary>

If a row has NULL value:
- `AVG(col)` ignores it (doesn't add to sum, doesn't increment count).
- `SUM(col) / COUNT(*)`: SUM ignores it, but COUNT(*) includes the row. This results in a smaller average (treating NULL as 0 effectively).
</details>

---

## Exercise 2 Hints

### Task 2.1 & 2.2: GROUP BY Fundamentals

<details>
<summary>Hint 1: The Golden Rule</summary>

If you `SELECT region, SUM(quantity)`, you MUST `GROUP BY region`.
If you `SELECT region, product_id, SUM(quantity)`, you MUST `GROUP BY region, product_id`.
</details>

<details>
<summary>Hint 2: Ordering by Aggregate</summary>

You can order by the result of an aggregation:
`ORDER BY SUM(quantity * unit_price) DESC`
</details>

### Task 2.3: Grouping by Expressions

<details>
<summary>Hint 1: Date functions</summary>

`EXTRACT(MONTH FROM sale_date)` or `TO_CHAR(sale_date, 'Month')`.
Remember: if you select the expression, you generally group by the same expression (or its column position or alias).
</details>

<details>
<summary>Hint 2: Conditional grouping</summary>

You can group by a CASE statement:
```sql
GROUP BY CASE 
  WHEN EXTRACT(ISODOW FROM sale_date) IN (6, 7) THEN 'Weekend'
  ELSE 'Weekday'
END
```
</details>

---

## Exercise 3 Hints

### Task 3.1: STRING_AGG

<details>
<summary>Hint 1: Syntax</summary>

`STRING_AGG(expression::text, delimiter)`
Example: `STRING_AGG(product_id::text, ', ')`
</details>

<details>
<summary>Hint 2: Distinct values in aggregation</summary>

You can use DISTINCT inside the aggregate:
`STRING_AGG(DISTINCT region, ', ')`
</details>

### Task 3.2: Filtered Aggregates

<details>
<summary>Hint: FILTER syntax</summary>

```sql
SUM(quantity * unit_price) FILTER (WHERE region = 'North')
```
This is standard SQL (supported by Postgres) and cleaner than `SUM(CASE WHEN region='North' THEN ... ELSE 0 END)`.
</details>

---

## Exercise 4 Hints

### Task 4.1: Counting Unique

<details>
<summary>Hint</summary>

`COUNT(DISTINCT product_id)`
</details>

### Task 4.3: Average of Distinct

<details>
<summary>Hint</summary>

1. First, find distinct products per day (Inner Query or CTE)
2. Then, take the average of those counts (Outer Query)

```sql
SELECT AVG(daily_count) FROM (
  SELECT sale_date, COUNT(DISTINCT product_id) as daily_count 
  FROM sales GROUP BY sale_date
) sub;
```
</details>

---

## Exercise 5 Hints

### Task 5.1: Grouping NULLs

<details>
<summary>Hint 1: NULL group</summary>

In `GROUP BY`, all NULLs are treated as a single group. You will see one row where the grouping column is NULL.
</details>

<details>
<summary>Hint 2: Replacing NULL in Group</summary>

If you want the output to say "Uncategorized" instead of NULL, use COALESCE in the SELECT list **and** (usually) group by the COALESCE expression or the column itself.

`SELECT COALESCE(subcategory, 'Uncategorized'), COUNT(*) ... GROUP BY 1`
</details>

---

## Exercise 6 Hints

### Challenge 6.3: Product Contribution

<details>
<summary>Hint: Calculating Percentage</summary>

You need the product's revenue AND the total revenue.
Since you can't easily mix aggregated (per product) and non-aggregated (total) in one simple query without window functions:

1. Calculate total revenue in a subquery: `(SELECT SUM(...) FROM sales)`
2. Use that value in your main query calculation: `product_revenue / (SELECT ...) * 100`

Alternatively, use a CTE.
</details>
