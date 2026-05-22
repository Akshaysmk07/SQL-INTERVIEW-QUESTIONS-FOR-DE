# Average Salary Department Wise — Oracle SQL Solution

## Approach: Using `AVG()` + `GROUP BY`

### Query

```sql
SELECT
    department,
    AVG(salary) AS avg_salary
FROM employees
GROUP BY department
ORDER BY AVG(salary) DESC;
```

---

# Explanation

## Step 1 — Group Employees Department Wise

```sql
GROUP BY department
```

Creates separate groups for each department.

Example:

- Engineering
- Finance
- HR

---

## Step 2 — Calculate Average Salary

```sql
AVG(salary)
```

Calculates the average salary within each department.

---

## Step 3 — Sort by Highest Average Salary

```sql
ORDER BY AVG(salary) DESC
```

Displays departments with highest average salary first.

---

# Output

| DEPARTMENT  | AVG_SALARY |
| ----------- | ---------- |
| Engineering | 85000      |
| Finance     | 80000      |
| HR          | 55000      |

---

# Department-Wise Calculation

## Engineering

| Salary |
| ------ |
| 90000  |
| 80000  |

Average:

:contentReference[oaicite:0]{index=0}

---

## Finance

| Salary |
| ------ |
| 75000  |
| 85000  |

Average:

:contentReference[oaicite:1]{index=1}

---

## HR

| Salary |
| ------ |
| 50000  |
| 60000  |

Average:

:contentReference[oaicite:2]{index=2}

---

# Important Oracle SQL Concepts

## `AVG()`

```sql
AVG(column_name)
```

Calculates average value of a numeric column.

---

## `GROUP BY`

Used to perform aggregation department-wise.

Without `GROUP BY`,
Oracle calculates average for the entire table.

---

## `ORDER BY`

Used to sort final aggregated results.

---

# Follow-Up Variations

## 1. Departments with Average Salary Above 70000

```sql
SELECT
    department,
    AVG(salary) AS avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 70000;
```

---

## 2. Highest Salary Per Department

```sql
SELECT
    department,
    MAX(salary) AS highest_salary
FROM employees
GROUP BY department;
```

---

## 3. Lowest Salary Per Department

```sql
SELECT
    department,
    MIN(salary) AS lowest_salary
FROM employees
GROUP BY department;
```

---

## 4. Employee Count Per Department

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department;
```

---

## 5. Departments Below Company Average Salary

```sql
SELECT
    department,
    AVG(salary) AS avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) < (
    SELECT AVG(salary)
    FROM employees
);
```

---

# Important Interview Concept

## Difference Between `WHERE` and `HAVING`

### `WHERE`

Filters rows before grouping.

### `HAVING`

Filters groups after aggregation.

Since average salary is an aggregate value:

```sql
HAVING AVG(salary) > 70000
```

must use `HAVING`, not `WHERE`.
