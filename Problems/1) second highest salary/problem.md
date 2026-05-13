# Second Highest Salary — LeetCode Style SQL Problem

## Problem Statement

Write a SQL query to find the **second highest distinct salary** from the `Employee` table.

If there is no second highest salary, return `NULL`.

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
(6, 'John', 120000);
```

---

## Expected Output

| SecondHighestSalary |
| ------------------- |
| 90000               |

---

## Constraints

* `1 <= Employee rows <= 10^5`
* Salary can contain duplicate values.
* Salary is always positive.

---

## Follow-Up Variations

1. Find the **Nth highest salary**
2. Find the **third highest salary**
3. Find employees earning the **highest salary in each department**
4. Find duplicate salaries
5. Solve without using `LIMIT`
