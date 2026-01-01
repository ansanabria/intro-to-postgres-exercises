# Section 1: Introduction - Hints

## Exercise 1.1 Hints

### Scenario A Hints

<details>
<summary>Hint 1: Basic Terminology</summary>

Think about the hierarchy: What contains what? A spreadsheet has multiple... which have multiple...

The smallest unit of data has a specific name. Each horizontal collection of these units also has a name.
</details>

<details>
<summary>Hint 2: Unique Identifiers</summary>

When something must be unique and is used to identify a specific record, there's a special term for it. Think about what "primary" means - it's the MAIN way to identify something.
</details>

<details>
<summary>Hint 3: Uniqueness Constraints</summary>

There's more than one way to ensure uniqueness. A primary key is one, but what if you need ANOTHER column to also be unique without it being the main identifier?
</details>

### Scenario B Hints

<details>
<summary>Hint 1: Minimum Tables</summary>

Think about the entities: What are the "nouns" in this scenario? Each major noun typically needs its own table.

But wait - how do you CONNECT them? Sometimes you need an additional table just for tracking relationships.
</details>

<details>
<summary>Hint 2: Relationship Types</summary>

Relationships are described by how many of one thing relates to another: 
- Can one member have many books? 
- Can one book have many members (at the same time)?

The answers determine the relationship type: one-to-one, one-to-many, or many-to-many.
</details>

<details>
<summary>Hint 3: Borrowing History</summary>

When you need to track the SAME relationship multiple times (member A borrowed book B in January AND in March), you need a different structure than just linking two tables directly.

What if you treated each "borrowing event" as its own entity?
</details>

---

## Exercise 1.2 Hints

### Scenario A Hints

<details>
<summary>Hint 1: Consider the Requirements</summary>

What does "data can be lost" tell you about the importance of durability? 

PostgreSQL excels at ACID compliance - but is that always necessary?
</details>

<details>
<summary>Hint 2: Alternative Solutions</summary>

What type of database is optimized for extremely fast reads/writes but trades off durability? Think about databases that keep everything in memory.
</details>

### Scenario B Hints

<details>
<summary>Hint 1: ACID Properties</summary>

ACID stands for four properties. Can you name them? Each one addresses a specific type of problem:
- A: What happens if an operation is interrupted?
- C: What happens if data violates rules?
- I: What happens when multiple operations occur simultaneously?
- D: What happens after a successful operation if the server crashes?
</details>

<details>
<summary>Hint 2: Concurrent Modifications</summary>

PostgreSQL uses a specific concurrency control method abbreviated MVCC. What does each letter stand for? How does creating "versions" help with concurrent access?
</details>

### Scenario C Hints

<details>
<summary>Hint 1: Flexible Data in PostgreSQL</summary>

PostgreSQL has native support for a data type that allows storing structured but flexible data. The column type you're looking for has two variants - one text-based, one binary.
</details>

<details>
<summary>Hint 2: Trade-offs</summary>

Consider: What do you gain by keeping everything in one database? What might you lose compared to a specialized document store?

Think about: querying capabilities, indexing, schema enforcement, joins with relational data.
</details>

---

## Exercise 1.3 Hints

### Client-Server Hints

<details>
<summary>Hint 1: Communication Protocol</summary>

When you use the Supabase SQL editor, your browser talks to Supabase's servers, which then talk to PostgreSQL. The PostgreSQL-specific protocol runs on a well-known port number (starts with 5).
</details>

### Database/Schema/Table Hints

<details>
<summary>Hint 1: Filing Cabinet Analogy</summary>

- Filing cabinet = ?
- Drawer = ?
- Folder = ?
- Papers in folder = ?

What's the default "drawer" called in PostgreSQL?
</details>

### Connections Hints

<details>
<summary>Hint 1: Connection Pooling</summary>

Creating a new connection to PostgreSQL is expensive (takes time and resources). If 1000 users each need their own connection, that's 1000 connections...

Connection pooling is like a library lending out books - you don't buy a new book for each reader.
</details>

---

## Exercise 1.4 Hints

### Situation 1 Hints

<details>
<summary>Hint 1: Orphaned References</summary>

If an order references product #123, but product #123 no longer exists, the order has a "dangling pointer." What database feature prevents deleting records that are referenced elsewhere?
</details>

<details>
<summary>Hint 2: Handling Options</summary>

When you CAN'T delete something because it's referenced, that's one option. But there are others:
- Set the reference to NULL
- Delete the referencing records too (cascade)
- Prevent the deletion (restrict)

These are called referential actions.
</details>

### Situation 2 Hints

<details>
<summary>Hint 1: The Problem</summary>

If both tellers check the balance simultaneously, both see $500. Both think they can withdraw $400. What's the final balance? This is a classic problem called...?
</details>

<details>
<summary>Hint 2: The Solution</summary>

Transactions with proper isolation prevent this. One transaction must complete before the other can see/modify the same data. Look up "transaction isolation levels."
</details>

### Situation 3 Hints

<details>
<summary>Hint 1: All or Nothing</summary>

The "A" in ACID stands for a word meaning "cannot be split." Either ALL operations succeed, or NONE do. What's that word?
</details>

<details>
<summary>Hint 2: Rollback</summary>

When a transaction fails partway through, PostgreSQL "undoes" all the changes made so far. This is called a rollback. The data returns to its state before the transaction began.
</details>

---

## General Study Tips

1. **Don't just memorize definitions** - understand WHY each concept exists and what problem it solves.

2. **Think of real-world analogies** - databases model real-world scenarios. If you can't explain a concept with a real-world example, you don't fully understand it.

3. **Consider failure cases** - most database concepts exist to prevent bad things from happening. Ask "what could go wrong without this?"

4. **Draw diagrams** - especially for relationships. Visual representations often clarify concepts better than text.
