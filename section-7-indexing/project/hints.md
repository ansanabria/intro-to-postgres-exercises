# Hints: The Performance Detective

## Part 1: The Feed Query

<details>
<summary>Hint 1: Foreign Keys</summary>

Index `posts(user_id)` and `follows(following_id)` and `follows(follower_id)`.
</details>

<details>
<summary>Hint 2: Sorting</summary>

The query orders by `created_at DESC`.
Index `posts(user_id, created_at DESC)` might allow Postgres to fetch posts for a user already sorted!
</details>

## Part 2: The Search Optimization

<details>
<summary>Hint</summary>

`LIKE '%text%'` has a leading wildcard. B-Trees sort from left to right. It's like finding a name ending in "son" in a phone book - you have to read every entry.
</details>
