# Exercise: Accessing JSONB Data

## Prerequisites
- Completed "Introduction to JSON"
- Populated `orders` table

---

## Exercise 1: Basic Operators (-> and ->>)

### Context
- `->` returns JSON object/array (intermediate result).
- `->>` returns text (final result).

### Tasks

#### Task 1.1: Extracting Fields
Select the customer's name (as text) and email (as text) from the `orders` table.

#### Task 1.2: Nested Extraction
Select the "newsletter" preference from the nested `customer_info` object.
- Hint: Chain the operators. `col -> 'key' ->> 'subkey'`

---

## Exercise 2: Array Access

### Context
JSON arrays are 0-indexed.

### Tasks

#### Task 2.1: First Item
Select the name of the *first* item in the `order_details` -> `items` array.

---

## Exercise 3: Filtering with @> (Containment)

### Context
The `@>` operator checks if the left JSON contains the right JSON. This is crucial for using GIN indexes efficiently.

### Tasks

#### Task 3.1: Finding Customers
Find all orders where the customer name is "John Doe".
- Use the containment operator: `customer_info @> ...`

#### Task 3.2: Finding Items
Find all orders that contain an item with "id": 1.
- Hint: `order_details @> '{"items": [{"id": 1}]}'`

---

## Exercise 4: Existence Operators (?, ?|, ?&)

### Context
Check if keys exist.

### Tasks

#### Task 4.1: Key Existence
Find orders where `customer_info` has a key called "preferences".

---

## Deliverables

For each exercise, provide:
1. SQL Query
2. Explanation of why you chose `->` vs `->>`
