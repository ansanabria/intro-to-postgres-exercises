# Exercise: Dates and Times

## Prerequisites
- Data Types knowledge

---

## Exercise 1: Understanding Timestamps

### Context
- `DATE`: YYYY-MM-DD
- `TIMESTAMP`: Date + Time
- `TIMESTAMP WITH TIME ZONE` (timestamptz): The gold standard for events.

### Tasks

#### Task 1.1: TZ Awareness
1. Create table `events` with `ts_raw TIMESTAMP` and `ts_tz TIMESTAMPTZ`.
2. Insert `NOW()` into both.
3. Change your session timezone (`SET TIME ZONE 'America/New_York';`).
4. Select the data back. Which one "moved" relative to UTC?

---

## Exercise 2: Intervals

### Context
Storing duration.

### Tasks

#### Task 2.1: The Subscription
Create a table `subscriptions` with `start_date` and `duration` (INTERVAL).
Insert a row starting today with duration '1 month'.
Calculate the end date in a SELECT query.

---

## Deliverables

For each exercise, provide:
1. SQL Query
2. Observation of timezone behavior
