# Hints: Dates and Times

## Exercise 1 Hints

### Task 1.1: TZ Awareness

<details>
<summary>Hint</summary>

`TIMESTAMPTZ` converts the input to UTC for storage, and converts back to the *session* timezone for display. `TIMESTAMP` ignores timezones completely (stores what you give it, returns what you gave it).
</details>
