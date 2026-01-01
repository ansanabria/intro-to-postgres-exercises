# PostgreSQL Exercises

A comprehensive set of challenging exercises for learning PostgreSQL, based on the [Intro to Postgres Course](https://databaseschool.com/series/intro-to-postgres/).

## Overview

This repository contains problem sets and projects designed to deepen your understanding of PostgreSQL concepts. Each section includes:

- **Exercises.md** - Problem sets for each topic requiring active application of concepts
- **Hints.md** - Guidance for working through exercises without giving away solutions
- **Project** - Cumulative projects combining all concepts learned in the section

## Structure

```
pg-exercises/
├── course-outline/
├── section-1-introduction/
├── section-2-querying-data/
│   ├── 01-exploring-data/
│   ├── 02-filtering/
│   ├── 03-operators-pattern-matching/
│   ├── 04-dealing-with-nulls/
│   ├── 05-aggregating-data/
│   ├── 06-having/
│   └── project/
├── section-3-joining-tables/
│   ├── 01-inner-joins/
│   ├── 02-left-joins/
│   ├── 03-right-joins/
│   ├── 04-orphaned-data/
│   ├── 05-unions/
│   └── project/
├── section-4-modifying-data/
│   ├── 01-inserting-data/
│   ├── 02-updating-data/
│   ├── 03-upserting-data/
│   ├── 04-returning-data/
│   ├── 05-deleting-records/
│   ├── 06-vacuuming/
│   └── project/
├── section-5-understanding-json/
│   ├── 01-introduction-to-json/
│   ├── 02-accessing-jsonb-data/
│   ├── 03-updating-json/
│   ├── 04-generated-columns-from-json/
│   └── project/
├── section-6-creating-tables/
│   ├── 01-guiding-principles/
│   ├── 02-data-types/
│   ├── 03-dates-and-times/
│   ├── 04-primary-keys/
│   ├── 05-check-constraints/
│   ├── 06-foreign-keys/
│   ├── 07-generated-columns/
│   └── project/
├── section-7-indexing/
│   ├── 01-intro-to-indexes/
│   ├── 02-characteristics-of-index/
│   ├── 03-btree-structure/
│   ├── 04-where-to-add-index/
│   ├── 05-composite-indexes/
│   ├── 06-explain/
│   └── project/
```

## Topics Covered

1. **Querying Data** - Exploring data, filtering, pattern matching, NULLs, aggregations, HAVING clause
2. **Joining Tables** - Inner joins, left joins, right joins, handling orphaned data, unions
3. **Modifying Data** - INSERT, UPDATE, UPSERT, RETURNING, DELETE, vacuuming
4. **Understanding JSON** - JSON introduction, JSONB access, updating JSON, generated columns
5. **Creating Tables** - Design principles, data types, dates/times, primary keys, constraints, foreign keys, generated columns
6. **Indexing** - Index fundamentals, B-tree structure, composite indexes, EXPLAIN

## Usage

1. Review the course material for a topic
2. Read `exercises.md` for the problem set
3. Attempt to solve exercises using PostgreSQL (e.g., Supabase managed instance)
4. Consult `hints.md` if stuck
5. Complete the section project to consolidate learning

## Requirements

- PostgreSQL database (Supabase or local installation)
- Basic understanding of SQL syntax
- A SQL client (psql, pgAdmin, DBeaver, or Supabase dashboard)
