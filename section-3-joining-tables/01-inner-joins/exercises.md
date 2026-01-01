# Exercise: Inner Joins

## Prerequisites
- Completed Section 2 (Querying Data)
- Understanding of basic table structures

## Setup

For Section 3, we'll need a more relational dataset. Run this SQL to create and populate the tables:

```sql
-- Create Department table
CREATE TABLE departments (
    department_id SERIAL PRIMARY KEY,
    department_name VARCHAR(100),
    location VARCHAR(100)
);

-- Create Employees table
CREATE TABLE employees (
    employee_id SERIAL PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(100),
    department_id INTEGER, -- FK to departments
    manager_id INTEGER,    -- Self-referencing FK
    hire_date DATE
);

-- Create Projects table
CREATE TABLE projects (
    project_id SERIAL PRIMARY KEY,
    project_name VARCHAR(100),
    start_date DATE,
    end_date DATE
);

-- Create Employee_Projects junction table (Many-to-Many)
CREATE TABLE employee_projects (
    employee_id INTEGER,
    project_id INTEGER,
    role VARCHAR(50),
    PRIMARY KEY (employee_id, project_id)
);

-- Populate Data
INSERT INTO departments (department_name, location) VALUES
('Engineering', 'Building A'),
('HR', 'Building B'),
('Sales', 'Building A'),
('Marketing', 'Building C');

INSERT INTO employees (first_name, last_name, email, department_id, manager_id, hire_date) VALUES
('John', 'Doe', 'john.doe@company.com', 1, NULL, '2020-01-15'),
('Jane', 'Smith', 'jane.smith@company.com', 1, 1, '2020-02-01'),
('Bob', 'Johnson', 'bob.johnson@company.com', 2, 1, '2019-05-20'),
('Alice', 'Williams', 'alice.williams@company.com', 3, 2, '2021-03-10'),
('Charlie', 'Brown', 'charlie.brown@company.com', NULL, 2, '2022-01-05'); -- NULL dept

INSERT INTO projects (project_name, start_date, end_date) VALUES
('Website Redesign', '2023-01-01', '2023-06-30'),
('Mobile App', '2023-03-01', '2023-12-31'),
('HR Portal', '2023-02-15', '2023-08-15');

INSERT INTO employee_projects (employee_id, project_id, role) VALUES
(1, 1, 'Tech Lead'),
(2, 1, 'Developer'),
(2, 2, 'Lead Developer'),
(3, 3, 'HR Specialist'),
(4, 2, 'Sales Rep');
```

---

## Exercise 1: Basic Inner Joins

### Context
INNER JOIN returns rows when there is a match in BOTH tables. If a record in Table A has no matching record in Table B, it is excluded.

### Tasks

#### Task 1.1: Employee Departments
Write a query to list all employees and their department names.
- Columns: First Name, Last Name, Department Name
- Requirement: Exclude employees with no department.

#### Task 1.2: Project Assignments
List all project assignments.
- Columns: Employee Name (Full Name), Project Name, Role
- Requirement: Use aliases for table names (e.g., `e`, `p`, `ep`).

---

## Exercise 2: Multi-Table Joins

### Context
You can chain multiple joins to connect several tables.

### Tasks

#### Task 2.1: Who works where and on what?
Create a master list showing:
- Employee Name
- Department Name
- Project Name
- Role in Project
- Location of the Department

Only include employees who are assigned to a department AND a project.

---

## Exercise 3: Join Conditions

### Context
Joins aren't limited to equality (`=`). You can join on complex conditions.

### Tasks

#### Task 3.1: Building Mates
Find pairs of departments that are located in the same building.
- Output: Dept 1 Name, Dept 2 Name, Location
- Constraint: Ensure you don't list the same pair twice (e.g., "Sales & Engineering" is same as "Engineering & Sales") and don't match a department with itself.

---

## Exercise 4: Self Joins

### Context
A table can be joined to itself. This is common for hierarchical data like managers and employees.

### Tasks

#### Task 4.1: Manager Names
List every employee and the name of their manager.
- Columns: Employee Name, Manager Name
- Hint: You'll need to join the `employees` table to the `employees` table. One instance represents the "employee", the other instance represents the "manager".

---

## Deliverables

For each exercise, provide:
1. SQL Query
2. Brief explanation of how the join works (especially for the self-join)
3. Number of rows returned
