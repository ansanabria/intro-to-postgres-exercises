# Hints: The NoSQL Hybrid Store

## Part 2: The Attribute Search

<details>
<summary>Hint 1: Finding Blue</summary>

`WHERE attributes @> '{"Color": "Blue"}'`
</details>

<details>
<summary>Hint 2: Has Storage</summary>

`WHERE attributes ? 'Storage'`
</details>

## Part 4: Reporting from JSON

<details>
<summary>Hint</summary>

```sql
SELECT 
  name, 
  COALESCE(attributes->>'CPU', attributes->>'Material', 'N/A') as main_spec
FROM products_hybrid;
```
</details>
