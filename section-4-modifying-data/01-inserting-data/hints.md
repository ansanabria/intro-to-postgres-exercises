# Hints: Inserting Data

## Exercise 1 Hints

### Task 1.3: Multi-Row Insert

<details>
<summary>Hint</summary>

```sql
INSERT INTO table (col1, col2) VALUES 
('val1', 'val2'),
('val3', 'val4'),
('val5', 'val6');
```
</details>

---

## Exercise 2 Hints

### Task 2.1: The Archive

<details>
<summary>Hint</summary>

`INSERT INTO target_table (col1, col2) SELECT col1, col2 FROM source_table WHERE ...`
</details>
