# Top 3 Salaries — LeetCode Style SQL Problem

## Problem Statement

Write a SQL query to find the **top 3 highest distinct salaries** from the `Employee` table.

Return the salaries in descending order.

---

## Table Schema

```sql
CREATE TABLE Employee (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    salary INT
);
```

---

## Sample Data

```sql
INSERT INTO Employee (id, name, salary) VALUES
(1, 'Akshay', 50000),
(2, 'Rahul', 70000),
(3, 'Sneha', 90000),
(4, 'Kiran', 70000),
(5, 'Meera', 120000),
(6, 'John', 120000),
(7, 'David', 85000),
(8, 'Anu', 95000);
```

---

## Expected Output

| salary |
| ------ |
| 120000 |
| 95000  |
| 90000  |

---

## Explanation

Distinct salaries in descending order:

```text
120000
95000
90000
85000
70000
50000
```

The top 3 highest distinct salaries are:

```text
120000
95000
90000
```

---

## Constraints

* `1 <= Employee rows <= 10^5`
* Salary can contain duplicate values
* Salary is always positive
* Output should contain only distinct salaries

---

## Follow-Up Variations

1. Find the top 5 salaries
2. Find top 3 salaries department-wise
3. Find employees earning top 3 salaries
4. Find the third highest salary
5. Solve without using `LIMIT`
