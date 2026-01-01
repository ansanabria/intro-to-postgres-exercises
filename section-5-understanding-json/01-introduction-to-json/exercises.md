# Exercise: Introduction to JSON

## Prerequisites
- Basic SQL knowledge

## Setup
Create a table to store JSON data.
```sql
CREATE TABLE orders (
    order_id SERIAL PRIMARY KEY,
    customer_info JSONB,
    order_details JSONB
);
```

---

## Exercise 1: JSON vs JSONB

### Context
PostgreSQL has two JSON types: `JSON` and `JSONB`.
- `JSON`: Stores exact text copy (preserves whitespace/key order). Fast write, slow read.
- `JSONB`: Stores binary format (indexed, no whitespace). Slower write, fast read.

### Tasks

#### Task 1.1: Insert Data
Insert a row into `orders` with the following structure:
- customer_info: `{"name": "John Doe", "email": "john@example.com", "preferences": {"newsletter": true}}`
- order_details: `{"items": [{"id": 1, "name": "Laptop", "price": 1200}, {"id": 2, "name": "Mouse", "price": 25}], "total": 1225}`

#### Task 1.2: The Duplicate Key Test
Try to insert a row where `customer_info` is `{"a": 1, "a": 2}`.
1. Does Postgres allow it?
2. If you SELECT it back, what value does "a" have?
3. Why does this happen with JSONB?

---

## Exercise 2: Structure Design

### Context
When to use columns vs JSON?

### Tasks

#### Task 2.1: Schema Critique
Critique this table design:
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    data JSONB -- {"username": "...", "password": "...", "email": "..."}
);
```
Why is this generally a bad idea compared to standard columns for core fields?

---

## Deliverables

For each exercise, provide:
1. SQL Query
2. Explanation of JSONB behavior
