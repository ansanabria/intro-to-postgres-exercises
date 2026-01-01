# Project: The E-Commerce Analytics Dashboard

## Overview
You have been hired as a Junior Data Engineer for "TechMart", a growing electronics retailer. Your manager needs a set of SQL queries to power a new internal dashboard that tracks sales performance, inventory health, and product trends.

This project requires you to apply ALL concepts learned in Section 2:
- Basic SELECT and aliases
- Filtering (WHERE) with complex conditions
- Pattern matching (LIKE/Regex)
- Handling NULLs
- Aggregation (COUNT, SUM, AVG)
- Grouping (GROUP BY) and Filtered Grouping (HAVING)

## The Data
You will use the `products` and `sales` tables created in the previous exercises. Ensure they are populated.

## Dashboard Requirements

### Part 1: Inventory Health Report
Create a query that flags products needing attention. The dashboard needs a list of products that meet **EITHER** of these criteria:
1. **Critical Low Stock**: Active products where stock is at or below the reorder level.
2. **Dead Stock**: Products that have never been sold (not present in sales table) OR haven't been restocked in the current year (2025) and have high stock (> 50).
   *(Note: Since we haven't learned JOINs yet, assume for the "never been sold" part that you might just check for NULLs or use basic filtering based on what we know. If you can't perfectly check "never sold" without joins, focus on the "no restock" criteria).*

**Output Columns**: Product Name, Stock Quantity, Status ('Critical' or 'Dead Stock' - hint: use CASE), Last Restocked Date.
**Order**: Critical items first, then by stock quantity ascending.

### Part 2: Regional Sales Performance
Management wants to know which regions are performing best, but they only care about "significant" regions.
1. Group sales by region.
2. Calculate:
   - Total Revenue
   - Number of unique products sold
   - Average Order Value
3. **Filter**: Only show regions with more than $500 in total revenue.
4. **Format**: Revenue should be formatted nicely (optional challenge, or just raw numbers).

### Part 3: The "Pareto" Product List
Identify the top-performing products that contribute most to sales.
1. Find products that have generated more than $100 in total revenue.
2. Exclude any "Office Supplies" (we only care about high-tech items for this report).
   *(Hint: You might need to filter by product IDs that you know are office supplies, or filter the raw data before grouping if you can match IDs).*
3. Order by Total Revenue descending.

### Part 4: Data Quality Audit
TechMart's data is messy. Write a query to find "Ghost Sales" or invalid records:
1. Sales where the `unit_price` in the sales table is significantly different (e.g., > 20% difference) from the current `price` in the products table.
   *(Note: This effectively requires joining logic. Since we are in Section 2, simplified version: Find sales where the unit_price is 0 or NULL, or where the region is NULL).*

### Part 5: Search Functionality
Build a query that simulates a user searching for "wireless" or "bluetooth" devices.
1. Return products matching "wireless" OR "bluetooth" (case insensitive) in name or description.
2. MUST currently be in stock.
3. Order by price (Low to High).

---

## Technical Constraints
- Use meaningful aliases for all calculated columns.
- Handle NULLs gracefully (e.g., display "Unknown Region" if region is NULL).
- Use comments to explain your logic.

## Submission
Create a file `solution.sql` containing the 5 queries, clearly labeled.
