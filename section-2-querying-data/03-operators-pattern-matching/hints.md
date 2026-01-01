# Hints: Operators and Pattern Matching

## Exercise 1 Hints

### Task 1.1: Basic LIKE Patterns

<details>
<summary>Hint 1: Starting with</summary>

To match "starts with X": `WHERE column LIKE 'X%'`

The `%` matches everything after X (including nothing).
</details>

<details>
<summary>Hint 2: Ending with</summary>

To match "ends with X": `WHERE column LIKE '%X'`

The `%` matches everything before X.
</details>

<details>
<summary>Hint 3: Contains</summary>

To match "contains X": `WHERE column LIKE '%X%'`

The `%` on both sides matches anything before and after X.
</details>

<details>
<summary>Hint 4: Exactly N characters before</summary>

The underscore `_` matches exactly ONE character. So `___` matches exactly 3 characters.

Pattern for exactly 3 characters before USB: `'___USB%'`
</details>

### Task 1.2: Single Character Wildcard

<details>
<summary>Hint 1: Fixed length patterns</summary>

`LIKE 'ELEC-__-001'` - each underscore is exactly one character.

For 10 characters total: `LIKE '__________'` (10 underscores) - but this is fragile. Consider using `LENGTH(column) = 10` instead.
</details>

### Task 1.3: Combining Wildcards

<details>
<summary>Hint: Starts with number</summary>

To match "starts with a digit", you need SIMILAR TO or regex. LIKE can't match "any digit".

With LIKE, you'd need: `LIKE '0%' OR LIKE '1%' OR ...` (tedious!)

Better: `WHERE description ~ '^[0-9]'` (regex)
</details>

### Task 1.4: Escaping Special Characters

<details>
<summary>Hint 1: ESCAPE clause</summary>

By default, `%` and `_` are wildcards. To search for literal `%`:

`WHERE name LIKE '%\%%' ESCAPE '\'`

The ESCAPE clause defines which character "escapes" the next character.
</details>

<details>
<summary>Hint 2: Underscore in names</summary>

To find literal underscore: `WHERE name LIKE '%\_%' ESCAPE '\'`

Look for 'Desk_Organizer_Pro' in the data.
</details>

---

## Exercise 2 Hints

### Task 2.1: ILIKE

<details>
<summary>Hint</summary>

Simply replace `LIKE` with `ILIKE` for case-insensitive matching:

`WHERE name ILIKE '%usb%'` matches 'USB', 'usb', 'Usb', etc.
</details>

### Task 2.2: Performance

<details>
<summary>Hint 1: Why ILIKE is slower</summary>

ILIKE must compare characters after converting case, which is extra work. It also cannot use a standard B-tree index efficiently.
</details>

<details>
<summary>Hint 2: Alternatives</summary>

1. Store normalized data: Keep a `name_lower` column that's always lowercase
2. Use a functional index: `CREATE INDEX ON products (LOWER(name))`
3. Use PostgreSQL's `citext` extension for case-insensitive text type
4. Use full-text search for complex searching
</details>

---

## Exercise 3 Hints

### Task 3.1: Basic Regex

<details>
<summary>Hint 1: Regex "starts with"</summary>

In regex, `^` anchors to the start: `WHERE name ~ '^USB'`

This is similar to `LIKE 'USB%'` but more powerful.
</details>

<details>
<summary>Hint 2: Only letters and spaces</summary>

`^[a-zA-Z ]+$` - matches strings containing ONLY letters and spaces:
- `^` = start
- `[a-zA-Z ]` = letter or space
- `+` = one or more
- `$` = end
</details>

### Task 3.2: Character Classes

<details>
<summary>Hint 1: Digit matching</summary>

`[0-9]` or `\d` matches any digit.

`WHERE name ~ '[0-9]'` finds names containing at least one digit.
</details>

<details>
<summary>Hint 2: Measurements</summary>

Pattern for "number followed by unit": `[0-9]+(cm|mm|m|kg)`

The `+` means one or more digits. The `(a|b|c)` means "a or b or c".
</details>

### Task 3.3: Quantifiers

<details>
<summary>Hint 1: Consecutive uppercase</summary>

`[A-Z]{2,}` matches 2 or more consecutive uppercase letters.

`{n}` = exactly n, `{n,}` = n or more, `{n,m}` = between n and m
</details>

<details>
<summary>Hint 2: Number range 10-99</summary>

You can't express numeric ranges directly in regex. Instead, match the pattern:
`[1-9][0-9]` matches 10-99 (first digit 1-9, second digit 0-9).

But be careful - this also matches if it's part of a larger number!
</details>

### Task 3.4: Alternation

<details>
<summary>Hint 1: Multiple options</summary>

`(cable|adapter)` matches either "cable" or "adapter".

For case-insensitive: use `~*` operator or include both cases in pattern.
</details>

<details>
<summary>Hint 2: Size patterns NxN</summary>

`[0-9]+x[0-9]+` matches patterns like "3x3", "90x40".

The `x` is literal, `[0-9]+` matches one or more digits.
</details>

---

## Exercise 4 Hints

### Task 4.1: Arithmetic

<details>
<summary>Hint: Calculations in SELECT</summary>

```sql
SELECT 
  name,
  price - cost AS profit,
  ROUND((price - cost) / price * 100, 1) AS margin_pct
FROM products
```

Remember to handle potential division by zero if price could be 0!
</details>

### Task 4.2: Modulo

<details>
<summary>Hint 1: Modulo operator</summary>

`%` is the modulo operator in PostgreSQL.

`WHERE product_id % 2 = 0` finds even IDs.
`WHERE stock_quantity % 25 = 0` finds quantities divisible by 25.
</details>

### Task 4.3: Division Types

<details>
<summary>Hint 1: Integer vs float division</summary>

- `5 / 2` = 2 (integer division, truncates)
- `5.0 / 2` = 2.5 (float division, preserves decimal)
- `5 / 2.0` = 2.5 (float division)
- `5::numeric / 2` = 2.5 (explicit cast)

If either operand is float/numeric, the result is float/numeric.
</details>

<details>
<summary>Hint 2: Division by zero</summary>

PostgreSQL throws an error on integer division by zero.

Use NULLIF to avoid: `stock / NULLIF(reorder_level, 0)` returns NULL if reorder_level is 0.
</details>

---

## Exercise 5 Hints

### Task 5.1: Concatenation

<details>
<summary>Hint 1: Concatenation operator</summary>

Use `||` to concatenate: `'[' || sku || '] - ' || name`

Or use `CONCAT()` function: `CONCAT('[', sku, '] - ', name)`
</details>

<details>
<summary>Hint 2: NULL handling</summary>

`||` returns NULL if ANY operand is NULL.
`CONCAT()` treats NULL as empty string.

To handle NULLs with `||`, use COALESCE:
`COALESCE(column, '') || '...'`
</details>

### Task 5.2: String Functions

<details>
<summary>Hint 1: Substring comparison</summary>

`LEFT(string, n)` gets first n characters.
`SUBSTRING(sku FROM 1 FOR 4)` also works.

Compare: `WHERE LEFT(sku, 4) != LEFT(category, 4)`
</details>

<details>
<summary>Hint 2: Length</summary>

`LENGTH(name)` returns number of characters.
`WHERE LENGTH(name) > 20`
</details>

### Task 5.3: Position

<details>
<summary>Hint 1: Finding position</summary>

`POSITION('USB' IN name)` returns position (1-indexed) or 0 if not found.

`STRPOS(name, 'USB')` does the same thing.
</details>

<details>
<summary>Hint 2: Extract until delimiter</summary>

`SPLIT_PART(sku, '-', 1)` splits by '-' and returns first part.

Or use substring with position:
`SUBSTRING(sku FROM 1 FOR POSITION('-' IN sku) - 1)`
</details>

---

## Exercise 6 Hints

### Challenge 6.1: Search Engine

<details>
<summary>Hint 1: Word matching</summary>

Split the search term into words, then check if ANY word matches:
`WHERE name ILIKE '%usb%' OR name ILIKE '%cable%' 
   OR description ILIKE '%usb%' OR description ILIKE '%cable%'`

For dynamic searches, you'd use string functions or full-text search.
</details>

<details>
<summary>Hint 2: Relevance ranking</summary>

Use CASE to assign scores:
```sql
ORDER BY (
  CASE WHEN name ILIKE '%search%' THEN 2 ELSE 0 END +
  CASE WHEN description ILIKE '%search%' THEN 1 ELSE 0 END
) DESC
```
</details>

### Challenge 6.2: SKU Validator

<details>
<summary>Hint 1: Validation regex</summary>

Valid pattern: `^(ELEC|FURN|OFSP)-[A-Z]{2}-[0-9]{3}$`

- `^` start
- `(ELEC|FURN|OFSP)` one of these
- `-` literal hyphen
- `[A-Z]{2}` exactly 2 uppercase letters
- `-` literal hyphen
- `[0-9]{3}` exactly 3 digits
- `$` end
</details>

<details>
<summary>Hint 2: Explaining why invalid</summary>

Use CASE to check each rule:
```sql
CASE 
  WHEN LENGTH(sku) != 11 THEN 'Wrong length'
  WHEN sku !~ '^(ELEC|FURN|OFSP)-' THEN 'Invalid prefix'
  WHEN ... THEN ...
END AS issue
```
</details>

### Challenge 6.3: Price Analysis

<details>
<summary>Hint 1: Round number check</summary>

A "round number" has no cents: `price = FLOOR(price)` or `price % 1 = 0`
</details>

<details>
<summary>Hint 2: Ends in .99</summary>

`(price * 100) % 100 = 99` or `price::text LIKE '%.99'`
</details>

---

## General Tips

1. **LIKE vs Regex**: Use LIKE for simple patterns. Use regex when you need character classes, quantifiers, or alternation.

2. **Performance**: Patterns starting with `%` can't use indexes efficiently. If possible, restructure to match from the start.

3. **Test regex**: Use `SELECT 'test string' ~ 'pattern'` to test your regex before applying to tables.

4. **Escape characters**: When searching for literal special characters, remember to escape them.
