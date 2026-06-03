# Rank Employees by Salary Department-Wise — MySQL Solution

## Approach: Using `RANK()`

### Query

```sql
SELECT
    department,
    employee_name,
    salary,
    RANK() OVER (
        PARTITION BY department
        ORDER BY salary DESC
    ) AS rank
FROM Employees
ORDER BY department, rank;
```

---

# Explanation

## Step 1 — Partition by Department

```sql
PARTITION BY department
```

Creates separate ranking groups for:

- Engineering
- Finance
- HR

Ranking restarts for each department.

---

## Step 2 — Rank by Salary

```sql
ORDER BY salary DESC
```

Highest salary receives Rank 1.

---

## Step 3 — Use `RANK()`

```sql
RANK() OVER (...)
```

Employees with the same salary receive the same rank.

Example:

| Employee | Salary | Rank |
| -------- | ------ | ---- |
| Akshay   | 90000  | 1    |
| John     | 90000  | 1    |
| Rahul    | 80000  | 3    |

Notice Rank 2 is skipped.

---

# Output

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

# Difference Between `RANK()` and `DENSE_RANK()`

## Using `RANK()`

| Salary | Rank |
| ------ | ---- |
| 90000  | 1    |
| 90000  | 1    |
| 80000  | 3    |

Ranks can have gaps.

---

## Using `DENSE_RANK()`

```sql
SELECT
    department,
    employee_name,
    salary,
    DENSE_RANK() OVER (
        PARTITION BY department
        ORDER BY salary DESC
    ) AS rank
FROM Employees;
```

| Salary | Rank |
| ------ | ---- |
| 90000  | 1    |
| 90000  | 1    |
| 80000  | 2    |

No gaps in ranking.

---

# Follow-Up Variations

## Top 3 Employees Per Department

```sql
SELECT *
FROM (
    SELECT e.*,
           RANK() OVER (
               PARTITION BY department
               ORDER BY salary DESC
           ) AS rnk
    FROM Employees e
) t
WHERE rnk <= 3;
```

---

## Second Highest Salary Per Department

```sql
SELECT *
FROM (
    SELECT e.*,
           DENSE_RANK() OVER (
               PARTITION BY department
               ORDER BY salary DESC
           ) AS rnk
    FROM Employees e
) t
WHERE rnk = 2;
```

---

## Employees with Rank Greater Than 3

```sql
SELECT *
FROM (
    SELECT e.*,
           RANK() OVER (
               PARTITION BY department
               ORDER BY salary DESC
           ) AS rnk
    FROM Employees e
) t
WHERE rnk > 3;
```

---

# Interview Tip

Use:

- `ROW_NUMBER()` → Unique ranking (1,2,3,4)
- `RANK()` → Same rank for ties, gaps allowed (1,1,3)
- `DENSE_RANK()` → Same rank for ties, no gaps (1,1,2)

For this problem, the expected output clearly indicates:

```sql
RANK()
```

because ranks jump from `1` to `3` after salary ties.
