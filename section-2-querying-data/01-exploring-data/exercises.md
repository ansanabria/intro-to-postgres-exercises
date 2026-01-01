# Exercise: Exploring the Data

## Prerequisites
- Understanding of basic database vocabulary (tables, rows, columns, etc.)
- Access to a PostgreSQL database (Supabase)

## Setup

Before starting these exercises, create and populate the following table in your database:

```sql
CREATE TABLE products (
    product_id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    category VARCHAR(50),
    subcategory VARCHAR(50),
    price DECIMAL(10, 2),
    cost DECIMAL(10, 2),
    stock_quantity INTEGER,
    reorder_level INTEGER,
    supplier_id INTEGER,
    weight_kg DECIMAL(6, 3),
    is_active BOOLEAN DEFAULT true,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    last_restocked DATE,
    description TEXT,
    sku VARCHAR(20) UNIQUE
);

INSERT INTO products (name, category, subcategory, price, cost, stock_quantity, reorder_level, supplier_id, weight_kg, is_active, last_restocked, description, sku) VALUES
('Wireless Mouse', 'Electronics', 'Peripherals', 29.99, 12.50, 150, 30, 1, 0.085, true, '2025-01-15', 'Ergonomic wireless mouse with USB receiver', 'ELEC-WM-001'),
('Mechanical Keyboard', 'Electronics', 'Peripherals', 89.99, 45.00, 75, 20, 1, 0.950, true, '2025-01-10', 'RGB mechanical keyboard with Cherry MX switches', 'ELEC-KB-001'),
('USB-C Hub', 'Electronics', 'Accessories', 49.99, 22.00, 200, 50, 2, 0.120, true, '2025-01-20', '7-in-1 USB-C hub with HDMI and SD card reader', 'ELEC-HB-001'),
('Monitor Stand', 'Furniture', 'Desk Accessories', 34.99, 15.00, 45, 15, 3, 2.500, true, '2024-12-28', 'Adjustable monitor stand with storage drawer', 'FURN-MS-001'),
('Desk Lamp', 'Furniture', 'Lighting', 24.99, 10.00, 0, 25, 3, 1.200, false, '2024-11-15', 'LED desk lamp with adjustable brightness', 'FURN-DL-001'),
('Webcam HD', 'Electronics', 'Peripherals', 59.99, 28.00, 90, 25, 1, 0.150, true, '2025-01-18', '1080p HD webcam with built-in microphone', 'ELEC-WC-001'),
('Office Chair', 'Furniture', 'Seating', 199.99, 95.00, 12, 5, 4, 15.000, true, '2024-12-01', 'Ergonomic office chair with lumbar support', 'FURN-CH-001'),
('Standing Desk', 'Furniture', 'Desks', 449.99, 220.00, 8, 3, 4, 35.000, true, '2024-11-20', 'Electric standing desk with memory presets', 'FURN-SD-001'),
('Notebook A5', 'Office Supplies', 'Paper Products', 4.99, 1.50, 500, 100, 5, 0.200, true, '2025-01-22', 'A5 lined notebook, 200 pages', 'OFSP-NB-001'),
('Pen Set', 'Office Supplies', 'Writing', 12.99, 4.00, 300, 75, 5, 0.100, true, '2025-01-22', 'Set of 10 ballpoint pens, assorted colors', 'OFSP-PN-001'),
('Laptop Stand', 'Electronics', 'Accessories', 39.99, 18.00, 60, 20, 2, 0.800, true, '2025-01-12', 'Aluminum laptop stand with cooling vents', 'ELEC-LS-001'),
('Wireless Charger', 'Electronics', 'Accessories', 19.99, 8.00, 180, 40, 2, 0.150, true, '2025-01-19', '15W fast wireless charging pad', 'ELEC-WCH-001'),
('Desk Organizer', 'Office Supplies', 'Storage', 14.99, 5.50, 120, 30, 5, 0.450, true, '2025-01-05', 'Wooden desk organizer with 5 compartments', 'OFSP-DO-001'),
('Cable Management Kit', 'Electronics', 'Accessories', 9.99, 3.00, 250, 60, 2, 0.200, false, NULL, 'Cable clips, ties, and sleeves bundle', 'ELEC-CM-001'),
('Ergonomic Mousepad', 'Electronics', 'Peripherals', 15.99, 6.00, 95, 30, 1, 0.300, true, '2025-01-08', 'Mousepad with gel wrist rest', 'ELEC-MP-001');
```

---

## Exercise 1: Understanding Your Data Structure

### Context
When working with a new database or table, the first step is always to understand what data you're working with. This means examining the structure, understanding the data types, and getting a feel for the actual content.

### Tasks

#### Task 1.1: Schema Exploration
Without querying the actual data, determine the following:
1. Write a query to list all columns in the `products` table along with their data types
2. Identify which columns can contain NULL values
3. Identify all constraints on this table (primary key, unique, etc.)

**Expected Understanding**: You should know how to inspect table structure using PostgreSQL's information schema or system catalogs.

#### Task 1.2: Data Sampling
Write queries to accomplish the following:
1. Retrieve exactly 5 random products (different each time you run)
2. Retrieve the first 10 products ordered by when they were added to the database
3. Retrieve 5 products, but skip the first 10 (pagination scenario)

**Challenge**: Explain why using `OFFSET` for pagination in large datasets might be problematic. What's a potential alternative?

---

## Exercise 2: Column Selection and Aliasing

### Context
Real-world queries rarely need all columns. Selecting only what you need improves performance and clarity. Aliasing makes output more readable, especially for calculated fields or when column names are technical.

### Tasks

#### Task 2.1: Selective Retrieval
Write a single query that displays:
- Product name (aliased as "Product")
- Category and subcategory combined as "Category > Subcategory" format (aliased as "Classification")
- Price formatted with currency symbol (aliased as "Retail Price")
- The profit per unit (price - cost), aliased as "Unit Margin"
- Profit margin percentage ((price - cost) / price * 100), aliased as "Margin %"

#### Task 2.2: Data Type Awareness
1. Write a query that would fail due to data type incompatibility, then fix it
2. Demonstrate the difference between `DECIMAL`, `INTEGER`, and `REAL` when calculating profit margins - which gives the most accurate results and why?

---

## Exercise 3: Ordering and Limiting Results

### Context
Ordering is fundamental for reports, pagination, and finding extremes. Understanding multi-column ordering and NULL handling in ORDER BY is essential.

### Tasks

#### Task 3.1: Complex Ordering
Write a query that orders products:
1. First by category (alphabetically)
2. Then by whether they're active (active products first)
3. Then by price (highest first)
4. Then by name (alphabetically) as a tiebreaker

#### Task 3.2: NULL Ordering Behavior
1. Write a query that shows all products ordered by `last_restocked`, with NULLs appearing FIRST
2. Write another version with NULLs appearing LAST
3. Explain the default behavior of PostgreSQL when ordering NULLs in ASC vs DESC

#### Task 3.3: Finding Extremes
Without using aggregate functions (MIN/MAX), write queries to find:
1. The single most expensive product
2. The 3 products with the lowest stock
3. The product with the highest profit margin

---

## Exercise 4: DISTINCT and Uniqueness

### Context
Understanding DISTINCT is crucial for getting unique values, but it's often misused. You need to understand how it works with multiple columns and its performance implications.

### Tasks

#### Task 4.1: Unique Values
1. Get all unique categories
2. Get all unique category-subcategory combinations
3. Count how many unique suppliers have products in the database

#### Task 4.2: DISTINCT ON (PostgreSQL-specific)
Write a query that returns only one product per category - specifically the most expensive product in each category. Use `DISTINCT ON`.

**Challenge**: Explain how `DISTINCT ON` differs from `GROUP BY` and when you would choose one over the other.

---

## Exercise 5: Comprehensive Data Exploration Challenge

### Context
You've just been given access to this products database and need to present a summary to your manager.

### Tasks
Write a SINGLE query for each of the following business questions:

1. **Inventory Value Report**: Show each product's name, the total inventory value (price × stock_quantity), and order by highest value first. Only show products with inventory value over $500.

2. **Reorder Alert**: Find all products where current stock is at or below the reorder level. Show product name, current stock, reorder level, and how many units below the reorder level they are (or 0 if at exactly the reorder level).

3. **Profitability Analysis**: Show the top 5 products by unit profit margin percentage, but only for active products with stock > 0. Include the product name, price, cost, and margin percentage rounded to 2 decimal places.

4. **Data Quality Check**: Find any products that might have data issues:
   - Price is less than or equal to cost (losing money)
   - Stock is negative
   - Reorder level is 0 or negative
   - Cost is NULL while price is set
   
   Show the product name, the issue column, and the problematic value.

---

## Deliverables

For each exercise, provide:
1. The complete SQL query
2. Sample output (first few rows)
3. Brief explanation of your approach

**Evaluation Criteria**:
- Query correctness and efficiency
- Proper use of column aliasing
- Understanding of data types and their implications
- Ability to handle edge cases (NULLs, empty results)
