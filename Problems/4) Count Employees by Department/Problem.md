# Count Employees by Department — LeetCode Style SQL Problem

## Problem Statement

Write a SQL query to count the number of employees in each department from the `Employee` table.

Return the department name along with the total employee count.

---

## Table Schema

```sql
CREATE TABLE Employee (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    department VARCHAR(100),
    salary INT
);
```

---

## Sample Data

```sql
INSERT INTO Employee (id, name, department, salary) VALUES
(1, 'Akshay', 'Engineering', 70000),
(2, 'Rahul', 'Engineering', 85000),
(3, 'Sneha', 'HR', 50000),
(4, 'Kiran', 'Finance', 90000),
(5, 'Meera', 'HR', 60000),
(6, 'John', 'Engineering', 95000),
(7, 'David', 'Finance', 75000);
```

---

## Expected Output

| department  | employee_count |
| ----------- | -------------- |
| Engineering | 3              |
| HR          | 2              |
| Finance     | 2              |

---

## Explanation

* Engineering department has 3 employees
* HR department has 2 employees
* Finance department has 2 employees

---

## Constraints

* `1 <= Employee rows <= 10^5`
* Department names are non-null
* Output order does not matter

---

## Follow-Up Variations

1. Find departments with more than 5 employees
2. Find average salary by department
3. Find highest salary in each department
4. Find departments with duplicate employee names
5. Count employees hired each year
