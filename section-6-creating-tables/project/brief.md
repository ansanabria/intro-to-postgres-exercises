# Project: The Library Schema

## Overview
You are designing the database schema for a public library system. You need to create tables that enforce strict data integrity rules using all the concepts learned in Section 6.

## Requirements

### Part 1: The Core Tables
Create the following tables with appropriate types and Primary Keys:
1. `members`: id, name, email, join_date.
2. `books`: id, title, isbn (13 chars), published_year.
3. `loans`: id, book_id, member_id, loan_date, due_date, return_date.

### Part 2: The Constraints
Add these constraints:
1. `books.isbn`: Must be exactly 13 characters.
2. `books.published_year`: Must be between 1000 and current year + 1.
3. `members.email`: Must be unique.
4. `loans.due_date`: Must be >= `loan_date`.

### Part 3: The Relationships
Add Foreign Keys:
1. `loans` links to `books` and `members`.
2. If a member is deleted, their loan history should NOT be deleted (Restrict or Set Null? Choose wisely).
   - *Logic*: We probably want to keep loan history for stats, but if a member is gone, maybe set member_id to NULL? Or forbid deleting members with active loans?
   - Decision: Implement `ON DELETE RESTRICT` (default) - can't delete member if they have loans.

### Part 4: The Smart Columns
1. Add a generated column to `loans`: `is_overdue` (boolean).
   - Logic: True if `return_date` is NULL AND `due_date` < Current Date?
   - *Limitation*: Generated columns can only reference other columns in the row, not "Current Date" (which changes).
   - *Alternative*: Add a generated column `days_loaned` calculated from `return_date - loan_date` (only valid if return_date is not null).

## Submission
Create `solution.sql` with the CREATE TABLE statements.
