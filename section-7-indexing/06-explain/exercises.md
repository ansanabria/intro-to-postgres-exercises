# Exercise: Explain

## Prerequisites
- Any query

---

## Exercise 1: Reading Plans

### Context
`EXPLAIN (ANALYZE, BUFFERS)` gives the most detail.

### Tasks

#### Task 1.1: The Deep Dive
Run `EXPLAIN (ANALYZE, BUFFERS)` on a simple query.
Identify:
1. The estimated cost (startup and total).
2. The actual time.
3. The number of "Buffers" (pages) read from memory vs disk.

---

## Deliverables

For each exercise, provide:
1. Annotated EXPLAIN output
