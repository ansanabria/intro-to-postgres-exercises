# Exercise: Operators and Pattern Matching

## Prerequisites
- Completed previous exercises (Exploring Data, Filtering)
- The `products` table with all previously inserted data

## Additional Setup

Add products with varied names for pattern matching exercises:

```sql
INSERT INTO products (name, category, subcategory, price, cost, stock_quantity, reorder_level, supplier_id, weight_kg, is_active, last_restocked, description, sku) VALUES
('USB-C to USB-A Adapter', 'Electronics', 'Cables', 7.99, 2.50, 200, 50, 2, 0.020, true, '2025-01-21', 'USB-C male to USB-A female adapter', 'ELEC-UA-001'),
('USB-C Cable 1m', 'Electronics', 'Cables', 8.99, 3.00, 250, 60, 2, 0.050, true, '2025-01-21', 'USB-C to USB-C cable, 1 meter', 'ELEC-UC-001'),
('USB 3.0 Hub', 'Electronics', 'Accessories', 24.99, 10.00, 85, 25, 2, 0.150, true, '2025-01-18', '4-port USB 3.0 hub with power adapter', 'ELEC-UH-001'),
('Mini USB Cable', 'Electronics', 'Cables', 5.99, 2.00, 100, 30, 2, 0.030, false, '2024-06-15', 'Mini USB to USB-A cable, legacy devices', 'ELEC-MU-001'),
('Desk_Organizer_Pro', 'Office Supplies', 'Storage', 29.99, 12.00, 40, 10, 5, 0.800, true, '2025-01-12', 'Premium desk organizer with charging dock', 'OFSP-DOP-001'),
('100W USB-C Charger', 'Electronics', 'Accessories', 45.99, 20.00, 60, 15, 2, 0.200, true, '2025-01-20', 'GaN 100W USB-C fast charger', 'ELEC-CH-001'),
('A4 Copy Paper (500 sheets)', 'Office Supplies', 'Paper Products', 6.99, 3.50, 1000, 200, 5, 2.500, true, '2025-01-22', 'A4 white copy paper, 80gsm, 500 sheets', 'OFSP-CP-001'),
('Post-it Notes 3x3"', 'Office Supplies', 'Paper Products', 4.49, 1.50, 300, 75, 5, 0.100, true, '2025-01-15', 'Yellow sticky notes, 100 sheets per pad', 'OFSP-PN-002'),
('50% Recycled Notebook', 'Office Supplies', 'Paper Products', 7.99, 3.00, 150, 40, 5, 0.300, true, '2025-01-10', 'Eco-friendly notebook, 50% recycled paper', 'OFSP-RN-001');
```

---

## Exercise 1: LIKE Pattern Matching

### Context
LIKE is the standard SQL pattern matching operator. It uses two wildcards:
- `%` matches any sequence of zero or more characters
- `_` matches exactly one character

### Tasks

#### Task 1.1: Basic LIKE Patterns
Write queries to find:
1. All products whose names start with 'USB'
2. All products whose names end with 'Cable'
3. All products containing 'USB' anywhere in the name
4. All products whose names contain exactly 3 characters before 'USB'

#### Task 1.2: Single Character Wildcard
1. Find products with SKUs that follow the pattern 'ELEC-XX-001' where XX is exactly 2 characters
2. Find products where the name has exactly 10 characters total
3. Find products with names that have a number as the second-to-last character

#### Task 1.3: Combining Wildcards
1. Find products whose descriptions start with a number followed by anything
2. Find products with SKUs like 'XXXX-YY-NNN' where XXXX is letters, YY is exactly 2 letters, and NNN is exactly 3 digits
3. Find products whose names start with a letter A-F and end with a digit

#### Task 1.4: LIKE Edge Cases
1. How do you search for products containing a literal `%` in their name?
2. How do you search for products containing a literal `_` in their name?
3. Search for the product with a name containing an underscore (there's one in the data)

---

## Exercise 2: ILIKE (Case-Insensitive)

### Context
ILIKE is PostgreSQL's case-insensitive version of LIKE. Understanding when to use it is important for user-facing searches.

### Tasks

#### Task 2.1: Case-Insensitive Searches
1. Find all products mentioning 'usb' regardless of case
2. Find products with categories that match 'electronics' regardless of how they're stored
3. Compare the results of `LIKE 'USB%'` vs `ILIKE 'usb%'`

#### Task 2.2: Performance Consideration
1. Explain why `ILIKE` might be slower than `LIKE`
2. If you needed case-insensitive matching with good performance, what alternatives could you consider? (Think about data normalization or indexing)

---

## Exercise 3: PostgreSQL Regular Expressions

### Context
PostgreSQL supports full regular expressions, which are far more powerful than LIKE. The operators are:
- `~` : matches regex (case-sensitive)
- `~*` : matches regex (case-insensitive)
- `!~` : does not match regex
- `!~*` : does not match regex (case-insensitive)

### Tasks

#### Task 3.1: Basic Regex Matching
1. Find products whose names start with 'USB' using regex
2. Find products whose names contain only letters and spaces (no numbers or special characters)
3. Find products with prices that have exactly 2 decimal places displayed (when cast to text)

#### Task 3.2: Character Classes
1. Find products with names containing any digit
2. Find products with SKUs starting with exactly 4 uppercase letters
3. Find products whose descriptions mention a measurement (number followed by 'cm', 'mm', 'm', or 'kg')

#### Task 3.3: Quantifiers and Anchors
1. Find products where the name has 2 or more consecutive uppercase letters
2. Find products with descriptions containing a number between 10 and 99
3. Find products with SKUs that end in exactly 3 digits

#### Task 3.4: Alternation and Grouping
1. Find products that are cables OR adapters (based on name)
2. Find products mentioning USB-A, USB-C, or USB-B in name or description
3. Find products with sizes mentioned (like "3x3", "90x40", any NxN pattern)

---

## Exercise 4: Arithmetic and Comparison Operators

### Context
Beyond pattern matching, understanding arithmetic and comparison operators is essential for data analysis.

### Tasks

#### Task 4.1: Arithmetic Calculations
Write queries showing:
1. All products with their profit per unit (price - cost)
2. All products with profit margin percentage, rounded to 1 decimal place
3. Products with inventory value (price × quantity) and cost value (cost × quantity)
4. The markup multiplier (price / cost) for each product

#### Task 4.2: Modulo Operations
1. Find products with an even product_id
2. Find products where stock_quantity is divisible by 25
3. Find products whose price, when rounded down to dollars, is divisible by 10

#### Task 4.3: Comparison Edge Cases
1. What's the result of `5 / 2` vs `5.0 / 2` vs `5 / 2.0`? Write queries to demonstrate.
2. What happens with division by zero in PostgreSQL? Test it.
3. Find products where `stock_quantity / reorder_level` exceeds 5 (be careful of division by zero!)

---

## Exercise 5: String Operators

### Context
PostgreSQL has powerful string manipulation operators that complement pattern matching.

### Tasks

#### Task 5.1: Concatenation
1. Create a full product label: "[SKU] - Name (Category > Subcategory)"
2. Create a price tag showing: "SALE: $XX.XX (was $YY.YY)" where YY.YY is 20% higher than the actual price
3. Handle NULL values in concatenation - what happens when you concatenate NULL?

#### Task 5.2: String Functions with Filtering
1. Find products where the first 4 characters of the SKU don't match the category's first 4 characters
2. Find products where name length exceeds 20 characters
3. Find products where the name and description share the first word

#### Task 5.3: Position and Extraction
1. Find the position of 'USB' in each product name (0 if not found)
2. Extract just the category code from SKUs (the first segment before the hyphen)
3. Find products where the description contains the product name (case-insensitive)

---

## Exercise 6: Challenge Problems

### Challenge 6.1: Search Engine Simulation
Build a product search query that:
- Accepts a search term 'usb cable'
- Matches if ANY word from the search appears in the name OR description
- Is case-insensitive
- Orders results by relevance (products matching in name should rank higher than description-only matches)

### Challenge 6.2: SKU Validator
Write a query that identifies products with invalid SKUs. A valid SKU must:
- Be exactly 11 characters
- Follow pattern: XXXX-YY-NNN
- First segment (XXXX) must be one of: ELEC, FURN, OFSP
- Second segment (YY) must be exactly 2 uppercase letters
- Third segment (NNN) must be exactly 3 digits

Show all products with invalid SKUs and explain WHY each is invalid.

### Challenge 6.3: Price Analysis
Create a comprehensive price analysis showing for each product:
- Name
- Price formatted as currency ($XX.XX)
- Price tier (Budget: < $20, Standard: $20-50, Premium: $50-100, Luxury: > $100)
- Whether price is a "round number" (no cents, like $50.00)
- Whether price ends in .99 (psychological pricing)
- Profit margin category (Low: <20%, Medium: 20-40%, High: >40%)

---

## Deliverables

For each exercise, provide:
1. Complete SQL query
2. Explanation of the pattern/operator used
3. Sample results
4. Any edge cases you discovered

**Evaluation Criteria**:
- Correct use of LIKE vs regex
- Understanding of wildcard behavior
- Proper handling of special characters
- Ability to combine patterns for complex matching
