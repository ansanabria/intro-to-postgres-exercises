# Project: The HR Analytics Suite

## Overview
HR needs a comprehensive view of the company structure. The existing data is scattered across tables. You need to use your mastery of Joins and Set Operations to build the ultimate HR report.

## The Data
Use the `employees`, `departments`, `projects`, and `employee_projects` tables.

## Requirements

### Part 1: The "Org Chart" View
Create a master query that lists every single employee with the following details:
- Employee Full Name
- Department Name (or 'Unassigned')
- Manager Name (or 'Top Level Management')
- Count of projects they are currently working on
- **Requirement**: Use Left Joins and Aggregate functions together.

### Part 2: Department Workload Analysis
We need to know how busy each department is.
- List all Departments.
- For each department, show:
  - Number of employees
  - Total number of project assignments for employees in that department
  - List of project names (comma separated) being worked on by that department
- **Requirement**: Include departments with 0 employees/projects (Left/Right joins).

### Part 3: Project Staffing Gaps
Identify projects that might be at risk.
- List all projects.
- Show the number of 'Lead' roles (roles containing 'Lead' or 'Manager') vs 'Execution' roles (everything else).
- Filter to show projects that have NO 'Lead' roles assigned.
- **Requirement**: This might require conditional aggregation (`SUM(CASE...)`) inside the join or subqueries.

### Part 4: The "Audit" Log (Unions)
Create a single list of "Entities" in the system to check for naming conflicts or just for search indexing.
- The list should include:
  - Employees (Name format: "User: First Last")
  - Departments (Name format: "Dept: Name")
  - Projects (Name format: "Proj: Name")
- Order the final list alphabetically.

### Part 5: Connectivity Check (Recursive Challenge - Optional/Bonus)
*Note: This might be advanced, but try thinking about it with Self Joins.*
Find all employees who are "2nd degree" connections to 'John Doe'.
- Meaning: John Doe -> works with Person A -> Person A works with Target.
- If too hard, find employees who share a project with someone who reports to 'John Doe'.

## Submission
Create `solution.sql` with the queries.
