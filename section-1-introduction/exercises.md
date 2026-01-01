# Section 1: Introduction - Exercises

## Overview
This section covers foundational concepts and vocabulary essential for working with PostgreSQL. Before diving into hands-on SQL, you must thoroughly understand the terminology and architecture of relational databases.

---

## Exercise 1.1: Database Vocabulary Mastery

### Context
Understanding database vocabulary is critical because these terms form the foundation of all database discussions, documentation, and problem-solving. Misunderstanding a term can lead to incorrect queries, poor schema design, or data integrity issues.

### Task
For each scenario below, identify ALL the relevant database terms that apply and explain WHY each term is relevant. Consider the relationships between terms.

#### Scenario A
You have a spreadsheet tracking employee information with columns for `employee_id`, `name`, `department`, `salary`, and `hire_date`. Each employee has a unique `employee_id`. You want to move this to PostgreSQL.

**Questions:**
1. What would each column become in database terminology? What is each individual piece of data called?
2. What would each row represent? What is the technical term?
3. What would the entire spreadsheet become?
4. The `employee_id` serves a special purpose - what database concept does it represent and why is it important?
5. If you wanted to ensure no two employees could have the same email address (a column you might add), what constraint concept would you use?

#### Scenario B
A library system needs to track books and the members who borrow them. One member can borrow many books, and each book can only be borrowed by one member at a time.

**Questions:**
1. How many tables would you minimally need? What would they represent?
2. What type of relationship exists between members and currently-borrowed books?
3. How would you establish this relationship in database terms?
4. If you wanted to track borrowing history (who borrowed what and when), how would this change your design? What new relationship type emerges?

---

## Exercise 1.2: PostgreSQL vs Other Databases - Critical Analysis

### Context
PostgreSQL was chosen for this course for specific reasons. Understanding these reasons helps you make informed decisions about when to use PostgreSQL and when another solution might be more appropriate.

### Task
Research and analyze the following scenarios. For each, determine whether PostgreSQL is a good fit and justify your reasoning based on PostgreSQL's characteristics.

#### Scenario A: Real-time Gaming Leaderboard
A mobile game needs to store player scores and display a real-time leaderboard. The system expects:
- 100,000+ concurrent players
- Score updates every few seconds per player
- Leaderboard queries every second
- Data can be lost if the server restarts (scores reset daily anyway)

**Questions:**
1. Is PostgreSQL the optimal choice here? Why or why not?
2. What PostgreSQL features would be beneficial? What would be problematic?
3. What alternative might you consider and why?

#### Scenario B: Financial Transaction System
A bank needs to store all customer transactions with complete accuracy. Requirements:
- Zero tolerance for data loss
- Must support complex queries for auditing
- Need to enforce business rules at the database level
- Must handle concurrent updates to account balances safely

**Questions:**
1. Is PostgreSQL suitable here? What specific features make it appropriate?
2. What does ACID compliance mean and why is it critical for this scenario?
3. How does PostgreSQL handle concurrent modifications to the same data?

#### Scenario C: Document Storage for a CMS
A content management system needs to store articles with varying structures - some have video embeds, some have image galleries, some are plain text with different metadata.

**Questions:**
1. Can PostgreSQL handle this? What feature specifically addresses varying document structures?
2. How does this compare to using a document database like MongoDB?
3. What are the trade-offs of using PostgreSQL's JSON capabilities vs a dedicated document store?

---

## Exercise 1.3: Architecture Understanding

### Context
Understanding how PostgreSQL is structured helps you troubleshoot issues, optimize performance, and understand error messages.

### Task
Answer the following questions about PostgreSQL architecture:

1. **Client-Server Model**: When you connect to your Supabase PostgreSQL instance, what is acting as the "client" and what is the "server"? What protocol do they use to communicate?

2. **Database vs Schema vs Table**: 
   - If PostgreSQL were a filing cabinet, what would be the database, schema, and table equivalents?
   - Can two tables in different schemas have the same name? What about two tables in the same schema?
   - What is the default schema in PostgreSQL?

3. **Connections and Sessions**:
   - When you run a query in the Supabase SQL editor, what happens at the connection level?
   - Why do managed services like Supabase use connection pooling?
   - What's the difference between a connection and a session?

---

## Exercise 1.4: Data Integrity Concepts

### Context
One of PostgreSQL's greatest strengths is maintaining data integrity. Understanding these concepts before writing any SQL is crucial.

### Task
For each situation, identify what could go wrong and what database concept would prevent the issue:

1. **Situation**: An e-commerce system allows orders to reference products. A developer deletes a product that has existing orders.
   - What problem occurs?
   - What database concept prevents this?
   - What are the different ways PostgreSQL can handle this situation?

2. **Situation**: Two bank tellers simultaneously process withdrawals from the same account that has $500. Each withdrawal is for $400.
   - What problem could occur without proper controls?
   - What database concept prevents this?
   - What does "isolation" mean in this context?

3. **Situation**: A user registration form submits data, but the application crashes after inserting the user but before inserting their default preferences.
   - What problem occurs?
   - What database concept prevents partial updates?
   - How does PostgreSQL handle this?

---

## Deliverables

For each exercise, provide:
1. Written answers demonstrating deep understanding
2. Real-world examples beyond those given
3. Connections between concepts where relevant

**Success Criteria**: You should be able to explain these concepts to someone else without referring to notes. If you can't, revisit the material.
