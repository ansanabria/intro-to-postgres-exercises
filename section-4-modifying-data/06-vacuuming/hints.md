# Hints: Vacuuming

## Exercise 1 Hints

### Task 1.1: Dead Tuples

<details>
<summary>Hint</summary>

Standard `VACUUM` marks space as "reusable" but doesn't return it to the OS (doesn't shrink file size) unless the dead tuples are at the physical end of the file.
</details>

### Task 1.2: Vacuum Full

<details>
<summary>Hint</summary>

`VACUUM FULL` rewrites the entire table to a new file, compacting it perfectly.
**Downside**: It takes an EXCLUSIVE LOCK, meaning no one else can read/write to the table while it runs.
</details>
