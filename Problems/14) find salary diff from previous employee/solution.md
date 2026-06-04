# Find Salary Difference from Previous Employee — MySQL Solution

## Approach: Using `LAG()`

### Query

```sql
SELECT
    employee_id,
    employee_name,
    salary,
    LAG(salary) OVER (
        ORDER BY salary
    ) AS previous_salary,
    salary -
    LAG(salary) OVER (
        ORDER BY salary
    ) AS salary_difference
FROM Employees
ORDER BY salary;
```

---

# Explanation

## Step 1 — Sort Employees by Salary

```sql
ORDER BY salary
```

Employees are arranged from lowest salary to highest salary.

| Employee | Salary |
| -------- | ------ |
| Akshay   | 50000  |
| Rahul    | 65000  |
| Sneha    | 75000  |
| Kiran    | 90000  |
| Meera    | 105000 |

---

## Step 2 — Get Previous Employee Salary

```sql
LAG(salary) OVER (
    ORDER BY salary
)
```

Returns the salary from the previous row.

For the first employee, no previous row exists, so `NULL` is returned.

---

## Step 3 — Calculate Salary Difference

```sql
salary -
LAG(salary) OVER (
    ORDER BY salary
)
```

Calculates:

```text
Current Salary - Previous Salary
```

---

# Output

| employee_id | employee_name | salary | previous_salary | salary_difference |
| ----------- | ------------- | ------ | --------------- | ----------------- |
| 1           | Akshay        | 50000  | NULL            | NULL              |
| 2           | Rahul         | 65000  | 50000           | 15000             |
| 3           | Sneha         | 75000  | 65000           | 10000             |
| 4           | Kiran         | 90000  | 75000           | 15000             |
| 5           | Meera         | 105000 | 90000           | 15000             |

---

# How `LAG()` Works

| Salary | Previous Salary |
| ------ | --------------- |
| 50000  | NULL            |
| 65000  | 50000           |
| 75000  | 65000           |
| 90000  | 75000           |
| 105000 | 90000           |

---

# Salary Difference Calculation

| Salary | Previous | Difference |
| ------ | -------- | ---------- |
| 50000  | NULL     | NULL       |
| 65000  | 50000    | 15000      |
| 75000  | 65000    | 10000      |
| 90000  | 75000    | 15000      |
| 105000 | 90000    | 15000      |

---

# Optimized Version (Avoid Calling `LAG()` Twice)

```sql
SELECT
    employee_id,
    employee_name,
    salary,
    previous_salary,
    salary - previous_salary AS salary_difference
FROM (
    SELECT
        employee_id,
        employee_name,
        salary,
        LAG(salary) OVER (
            ORDER BY salary
        ) AS previous_salary
    FROM Employees
) t
ORDER BY salary;
```

This version is generally preferred in interviews because the window function is evaluated only once.

---

# Follow-Up Variations

## 1. Salary Difference Within Each Department

```sql
SELECT
    employee_id,
    employee_name,
    department,
    salary,
    LAG(salary) OVER (
        PARTITION BY department
        ORDER BY salary
    ) AS previous_salary
FROM Employees;
```

---

## 2. Find Next Employee Salary (`LEAD()`)

```sql
SELECT
    employee_id,
    employee_name,
    salary,
    LEAD(salary) OVER (
        ORDER BY salary
    ) AS next_salary
FROM Employees;
```

---

## 3. Percentage Salary Growth

```sql
SELECT
    employee_id,
    employee_name,
    salary,
    previous_salary,
    ROUND(
        (salary - previous_salary)
        * 100.0 / previous_salary,
        2
    ) AS percentage_growth
FROM (
    SELECT *,
           LAG(salary) OVER (
               ORDER BY salary
           ) AS previous_salary
    FROM Employees
) t;
```

---

## 4. Employees Whose Salary Increased by More Than 20000

```sql
SELECT *
FROM (
    SELECT
        employee_id,
        employee_name,
        salary,
        salary -
        LAG(salary) OVER (
            ORDER BY salary
        ) AS salary_difference
    FROM Employees
) t
WHERE salary_difference > 20000;
```

---

# Interview Tip

Remember these three common window-function patterns:

| Requirement        | Function                                       |
| ------------------ | ---------------------------------------------- |
| Previous row value | `LAG()`                                      |
| Next row value     | `LEAD()`                                     |
| Rank rows          | `RANK()`, `DENSE_RANK()`, `ROW_NUMBER()` |

For problems involving **comparison with the previous record**, `LAG()` is almost always the expected solution.
