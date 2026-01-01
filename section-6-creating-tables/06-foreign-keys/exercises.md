# Exercise: Foreign Keys

## Prerequisites
- Primary Keys

---

## Exercise 1: Relationships

### Context
Foreign Keys enforce referential integrity.

### Tasks

#### Task 1.1: The Author-Book Link
1. Create table `authors` (id pk, name).
2. Create table `books` (id pk, title, author_id).
3. Add a Foreign Key on `books.author_id` referencing `authors.id`.

#### Task 1.2: Delete Cascade
1. Try to delete an author who has books. (Should fail).
2. Re-create the FK with `ON DELETE CASCADE`.
3. Delete the author again. What happens to the books?

---

## Deliverables

For each exercise, provide:
1. SQL Query
2. Observation of Cascade behavior
