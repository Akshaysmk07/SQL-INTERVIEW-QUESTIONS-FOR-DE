# Find Salary Difference from Previous Employee — MySQL LeetCode Style Problem

## Problem Statement

Write a MySQL query to display each employee along with the difference between their salary and the salary of the previous employee when employees are ordered by salary.

Return:

* Employee ID
* Employee Name
* Salary
* Previous Employee Salary
* Salary Difference

For the employee with the lowest salary, the previous salary should be `NULL`, and the salary difference should also be `NULL`.

Sort the output by salary in ascending order.

---

## Table Schema

```sql
CREATE TABLE Employees (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(100),
    salary INT
);
```

---

## Sample Data

```sql
INSERT INTO Employees (employee_id, employee_name, salary) VALUES
(1, 'Akshay', 50000),
(2, 'Rahul', 65000),
(3, 'Sneha', 75000),
(4, 'Kiran', 90000),
(5, 'Meera', 105000);
```

---

## Expected Output

| employee_id | employee_name | salary | previous_salary | salary_difference |
| ----------- | ------------- | ------ | --------------- | ----------------- |
| 1           | Akshay        | 50000  | NULL            | NULL              |
| 2           | Rahul         | 65000  | 50000           | 15000             |
| 3           | Sneha         | 75000  | 65000           | 10000             |
| 4           | Kiran         | 90000  | 75000           | 15000             |
| 5           | Meera         | 105000 | 90000           | 15000             |

---

## Explanation

Employees sorted by salary:

| Employee | Salary |
| -------- | ------ |
| Akshay   | 50000  |
| Rahul    | 65000  |
| Sneha    | 75000  |
| Kiran    | 90000  |
| Meera    | 105000 |

* Rahul's salary difference = 65000 − 50000 = 15000
* Sneha's salary difference = 75000 − 65000 = 10000
* Kiran's salary difference = 90000 − 75000 = 15000
* Meera's salary difference = 105000 − 90000 = 15000

---

## Constraints

* `1 <= Employees rows <= 10^5`
* Salaries are positive integers.
* Multiple employees may have the same salary.
* Output should be sorted by salary.

---

## Follow-Up Variations

1. Find salary difference within each department.
2. Find salary difference from the next employee using `LEAD()`.
3. Calculate percentage salary growth from the previous employee.
4. Find employees whose salary increased by more than 20,000 compared to the previous one.
5. Rank employees by salary and display the difference from the previous rank.
