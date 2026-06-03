# Rank Employees by Salary Department-Wise — MySQL LeetCode Style Problem

## Problem Statement

Write a MySQL query to rank employees based on their salary within each department.

* Employees with the same salary should receive the same rank.
* Ranking should restart for each department.
* Return the department, employee name, salary, and rank.
* Sort the output by department and rank.

---

## Table Schema

```sql
CREATE TABLE Employees (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(100),
    department VARCHAR(100),
    salary INT
);
```

---

## Sample Data

```sql
INSERT INTO Employees (employee_id, employee_name, department, salary) VALUES
(1, 'Akshay', 'Engineering', 90000),
(2, 'Rahul', 'Engineering', 80000),
(3, 'John', 'Engineering', 90000),
(4, 'Sneha', 'HR', 70000),
(5, 'Meera', 'HR', 60000),
(6, 'David', 'Finance', 85000),
(7, 'Kiran', 'Finance', 85000),
(8, 'Anu', 'Finance', 75000);
```

---

## Expected Output

| department  | employee_name | salary | rank |
| ----------- | ------------- | ------ | ---- |
| Engineering | Akshay        | 90000  | 1    |
| Engineering | John          | 90000  | 1    |
| Engineering | Rahul         | 80000  | 3    |
| Finance     | David         | 85000  | 1    |
| Finance     | Kiran         | 85000  | 1    |
| Finance     | Anu           | 75000  | 3    |
| HR          | Sneha         | 70000  | 1    |
| HR          | Meera         | 60000  | 2    |

---

## Explanation

### Engineering

| Employee | Salary | Rank |
| -------- | ------ | ---- |
| Akshay   | 90000  | 1    |
| John     | 90000  | 1    |
| Rahul    | 80000  | 3    |

### Finance

| Employee | Salary | Rank |
| -------- | ------ | ---- |
| David    | 85000  | 1    |
| Kiran    | 85000  | 1    |
| Anu      | 75000  | 3    |

### HR

| Employee | Salary | Rank |
| -------- | ------ | ---- |
| Sneha    | 70000  | 1    |
| Meera    | 60000  | 2    |

---

## Constraints

* `1 <= Employees rows <= 10^5`
* Salary is always positive.
* Multiple employees can have the same salary.
* Ranking should be calculated separately for each department.

---

## Follow-Up Variations

1. Use `DENSE_RANK()` instead of `RANK()`.
2. Find the top 3 employees per department.
3. Find the second-highest salary in each department.
4. Rank employees by joining date department-wise.
5. Find employees whose rank is greater than 3.
