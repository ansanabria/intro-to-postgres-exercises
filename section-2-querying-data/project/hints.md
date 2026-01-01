# Hints: E-Commerce Analytics Dashboard

## Part 1: Inventory Health Report

<details>
<summary>Hint 1: Combining Logic</summary>

You'll need a complex WHERE clause with OR:
`WHERE (condition_for_critical) OR (condition_for_dead_stock)`
</details>

<details>
<summary>Hint 2: Status Column</summary>

Use a CASE statement in the SELECT clause to create the 'Status' label based on the same logic used in the WHERE clause.
</details>

## Part 2: Regional Sales Performance

<details>
<summary>Hint 1: "Significant" Regions</summary>

Filtering groups (regions) based on an aggregate (total revenue) requires `HAVING`.
</details>

## Part 3: The "Pareto" Product List

<details>
<summary>Hint 1: Filtering Categories</summary>

Since we can't JOIN yet to check category names from the sales table directly (unless we assume sales has product details, which it usually doesn't), you might have to filter by known ID ranges or just perform the aggregation on the sales table and filter by `product_id` if you know which ones are office supplies. 
*Self-correction*: Actually, if you are selecting FROM products, you can filter by category. But to get "total revenue", you need sales data.
*Strategy*: Stick to querying the `sales` table for revenue, and maybe manually filter out IDs 9, 10, 13 (Office Supplies) using `WHERE product_id NOT IN (...)`.
</details>

## Part 4: Data Quality Audit

<details>
<summary>Hint</summary>

Focus on the `sales` table anomalies.
`WHERE unit_price IS NULL OR unit_price = 0 OR region IS NULL`
</details>

## Part 5: Search Functionality

<details>
<summary>Hint</summary>

Use `ILIKE` for case-insensitive matching.
`WHERE (name ILIKE '%wireless%' OR description ILIKE '%wireless%' ...) AND stock_quantity > 0`
</details>
