# Highest Paid Employee Per Department — LeetCode Style SQL Problem

## Problem Statement

Write a SQL query to find the employee(s) who earn the highest salary in each department.

Return the department name, employee name, and salary.

If multiple employees have the same highest salary in a department, return all of them.

---

## Table Schema

```sql
CREATE TABLE Employee (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(100),
    department VARCHAR(100),
    salary INT
);
```

---

## Sample Data

```sql
INSERT INTO Employee (employee_id, employee_name, department, salary) VALUES
(1, 'Akshay', 'Engineering', 95000),
(2, 'Rahul', 'Engineering', 85000),
(3, 'Sneha', 'HR', 70000),
(4, 'Kiran', 'Finance', 90000),
(5, 'Meera', 'HR', 70000),
(6, 'John', 'Engineering', 95000),
(7, 'David', 'Finance', 75000);
```

---

## Expected Output

| department  | employee_name | salary |
| ----------- | ------------- | ------ |
| Engineering | Akshay        | 95000  |
| Engineering | John          | 95000  |
| HR          | Sneha         | 70000  |
| HR          | Meera         | 70000  |
| Finance     | Kiran         | 90000  |

---

## Explanation

* Engineering highest salary is `95000` → Akshay and John
* HR highest salary is `70000` → Sneha and Meera
* Finance highest salary is `90000` → Kiran

---

## Constraints

* `1 <= Employee rows <= 10^5`
* Salary is always positive
* Department names are non-null
* Multiple employees can share the same highest salary

---

## Follow-Up Variations

1. Find second highest salary per department
2. Find top 3 salaries in each department
3. Find lowest paid employee per department
4. Find average salary by department
5. Find departments where highest salary exceeds 1 lakh
