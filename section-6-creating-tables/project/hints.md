# Hints: The Library Schema

## Part 2: The Constraints

<details>
<summary>Hint</summary>

- ISBN: `CHAR(13)` or `CHECK (LENGTH(isbn) = 13)`
- Year: `CHECK (published_year BETWEEN ...)`
- Unique: `UNIQUE (email)`
- Date: `CHECK (due_date >= loan_date)`
</details>

## Part 4: Smart Columns

<details>
<summary>Hint</summary>

Correct, you cannot use `NOW()` in generated columns.
Stick to `days_loaned`:
`GENERATED ALWAYS AS (return_date - loan_date) STORED`
</details>
