# Exercise: Primary Keys

## Prerequisites
- `CREATE TABLE`

---

## Exercise 1: Natural vs Surrogate Keys

### Context
- Natural Key: Real-world data unique to the row (e.g., SSN, Email).
- Surrogate Key: Artificial ID (e.g., Serial, UUID).

### Tasks

#### Task 1.1: Defining PKs
Create a table `students` where `student_id` is a SERIAL PRIMARY KEY.

#### Task 1.2: Composite Keys
Create a table `class_enrollments` where the combination of `student_id` and `class_id` is the Primary Key.
- Syntax: `PRIMARY KEY (col1, col2)`

---

## Deliverables

For each exercise, provide:
1. SQL Query
