# Project: The Performance Detective

## Overview
You have inherited a slow database for a "Social Media" app. Users are complaining that the news feed is slow. You need to identify missing indexes and optimize the schema.

## The Data
Create and populate these tables (with significant data, e.g., 100k rows):
1. `users`: id, username, email, created_at.
2. `posts`: id, user_id, content, created_at, likes_count.
3. `follows`: follower_id, following_id, created_at.

## Requirements

### Part 1: The Feed Query
The main query is:
```sql
SELECT p.content, u.username, p.created_at
FROM posts p
JOIN users u ON p.user_id = u.id
JOIN follows f ON p.user_id = f.following_id
WHERE f.follower_id = 1
ORDER BY p.created_at DESC
LIMIT 20;
```
(Logic: Show posts from people User 1 follows).

1. Run `EXPLAIN ANALYZE` on this query.
2. Identify the bottlenecks (Seq Scans, high costs).
3. Create indexes to optimize:
   - The Join conditions.
   - The filtering (`follower_id`).
   - The Sorting (`created_at`).

### Part 2: The Search Optimization
Users search for posts containing specific words.
`SELECT * FROM posts WHERE content LIKE '%database%';`
1. Explain why a standard B-Tree index on `content` won't help here.
2. (Bonus/Research): What Postgres index type *would* help with Full Text Search? (Hint: GIN/GiST with tsvector, though just mentioning the limitation of B-Tree is enough for this scope).

### Part 3: The Analytics
Marketing runs this query constantly:
`SELECT date_trunc('day', created_at), COUNT(*) FROM posts GROUP BY 1;`
1. Can an index help this Group By aggregation?
2. Create an index on `created_at` and check if an "Index Only Scan" or similar optimization occurs.

## Submission
Create `solution.sql` containing:
1. The schema creation script.
2. The "Before" EXPLAIN output.
3. The `CREATE INDEX` statements.
4. The "After" EXPLAIN output showing improvement.
