# Exercise: Guiding Principles of Table Design

## Prerequisites
- Basic understanding of what a table is

---

## Exercise 1: Normalization Thinking

### Context
Normalization reduces redundancy.

### Tasks

#### Task 1.1: The Bad Table
Consider this table for a Blog:
`posts (id, title, content, author_name, author_email, author_bio)`

1. Identify the problem with this design if an author writes 100 posts.
2. Propose a normalized design using two tables. Write the `CREATE TABLE` statements (conceptual is fine, precise syntax not required yet).

---

## Exercise 2: Naming Conventions

### Context
Consistency is key. Postgres is case-insensitive (unless quoted), so snake_case is standard.

### Tasks

#### Task 2.1: Fix the Names
Refactor these proposed column names to standard Postgres conventions:
- `CustomerName`
- `dateOfBirth`
- `Shipping Address`
- `Order ID`

---

## Deliverables

For each exercise, provide:
1. Written answers
2. Proposed Schema (SQL)
