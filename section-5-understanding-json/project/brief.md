# Project: The NoSQL Hybrid Store

## Overview
You are building the product catalog for a flexible e-commerce platform. The requirement is to store products that vary wildly in their attributes (e.g., T-shirts have size/color, Laptops have RAM/CPU, Books have ISBN/Author). A rigid relational schema won't work well for the attributes. You decide to use a Hybrid approach: Relational columns for common data, JSONB for flexible attributes.

## The Data
Create a table `products_hybrid`:
- `id` (Serial, PK)
- `name` (Text)
- `category` (Text)
- `attributes` (JSONB) - stores things like color, size, tech specs
- `metadata` (JSONB) - stores supplier info, tags, release year

## Requirements

### Part 1: The Flexible Insert
Insert 3 distinct products with different attribute structures:
1. A T-Shirt (Size: L, Color: Blue, Material: Cotton)
2. A Laptop (CPU: i7, RAM: 16GB, Storage: 512GB)
3. A Smartphone (Color: Black, Storage: 128GB, 5G: true)

### Part 2: The Attribute Search
Write queries to find:
1. All products that are "Blue" (regardless of whether they are shirts or phones).
2. All products that have "Storage" capacity defined (Laptops, Phones).
3. **Challenge**: Find products where the "Storage" is "512GB" OR "128GB".

### Part 3: The Bulk Update
Management decided to standardize tag names.
1. In the `metadata` column, if there is a "tags" array containing "mobile", append "portable" to that array.
   - Hint: You might need to check containment (`@>`) first.
   - This effectively requires reading the array, modifying it, and updating it back.

### Part 4: Reporting from JSON
Create a summary report showing:
- Product Name
- Category
- A column "Main Spec" that displays:
  - The "CPU" if it exists
  - The "Material" if it exists
  - Or "N/A" if neither exists.
- **Requirement**: Use `COALESCE` with JSON extraction operators.

### Part 5: Indexing Strategy
1. Create a GIN index on the `attributes` column.
2. Write a query searching for a specific key-value pair (`{"Color": "Blue"}`) and explain why the index would help here.

## Submission
Create `solution.sql`.
