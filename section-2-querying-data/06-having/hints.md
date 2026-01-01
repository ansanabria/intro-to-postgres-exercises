# Hints: Having

## Exercise 1 Hints

### Task 1.1: Filtering Before vs After

<details>
<summary>Hint 1: Order of Operations</summary>

SQL Order of Execution:
1. FROM
2. WHERE (Row filtering)
3. GROUP BY
4. HAVING (Group filtering)
5. SELECT
</details>

<details>
<summary>Hint 2: Why WHERE fails</summary>

The database scans rows one by one. At the "WHERE" stage, it hasn't grouped anything yet, so it doesn't know the "sum" of a group. That's why `WHERE SUM(...)` is illegal.
</details>

---

## Exercise 2 Hints

### Task 2.1: Revenue Thresholds

<details>
<summary>Hint</summary>

`GROUP BY region HAVING SUM(quantity * unit_price) > 1000`
</details>

---

## Exercise 3 Hints

### Task 3.2: Aggregates in HAVING only

<details>
<summary>Hint</summary>

Yes, it is valid! You can filter by criteria you don't display.
`SELECT region FROM sales GROUP BY region HAVING AVG(unit_price) > 50`
</details>

---

## Exercise 4 Hints

### Challenge 4.3: The "Average" Region

<details>
<summary>Hint: Subquery in HAVING</summary>

You can compare an aggregate to a scalar subquery.

```sql
HAVING AVG(quantity * unit_price) < (
    SELECT AVG(quantity * unit_price) FROM sales
)
```
</details>
