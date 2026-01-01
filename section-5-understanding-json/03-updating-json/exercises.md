# Exercise: Updating JSON

## Prerequisites
- Populated `orders` table

---

## Exercise 1: jsonb_set

### Context
Modifying a specific key inside a JSONB column.

### Tasks

#### Task 1.1: Updating a Field
Update the order with ID 1. Change "John Doe" to "Jane Doe" in `customer_info`.
- Use `jsonb_set(target, path, new_value, create_missing)`.

#### Task 1.2: Adding a Field
Add a new field "phone": "555-0199" to `customer_info` for order 1.

---

## Exercise 2: Removing Keys

### Context
Using the `-` operator.

### Tasks

#### Task 2.1: The Cleanup
Remove the "preferences" key from `customer_info` for all orders.

---

## Exercise 3: Array Modification

### Context
Appending to arrays uses `||`.

### Tasks

#### Task 3.1: Add Item
Add a new item `{"id": 3, "name": "Cable", "price": 10}` to the `items` array in `order_details` for order 1.

---

## Deliverables

For each exercise, provide:
1. SQL Query
2. Sample data showing the change
