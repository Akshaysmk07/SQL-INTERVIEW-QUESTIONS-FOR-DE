# Highest Paid Employee Per Department — SQL Solution

## Approach 1: Using `DENSE_RANK()`

### Query

```sql
SELECT
    department,
    employee_name,
    salary
FROM (
    SELECT *,
           DENSE_RANK() OVER (
               PARTITION BY department
               ORDER BY salary DESC
           ) AS rnk
    FROM Employee
) tab
WHERE rnk = 1;
```

---

# Explanation

## Step 1 — Partition Employees by Department

```sql
PARTITION BY department
```

Separates employees department-wise.

Each department gets ranked independently.

---

## Step 2 — Rank Salaries in Descending Order

```sql
ORDER BY salary DESC
```

Highest salary gets rank `1`.

---

## Step 3 — Use `DENSE_RANK()`

```sql
DENSE_RANK()
```

Handles salary ties properly.

Example:

| department  | employee_name | salary | rank |
| ----------- | ------------- | ------ | ---- |
| Engineering | Akshay        | 95000  | 1    |
| Engineering | John          | 95000  | 1    |
| Engineering | Rahul         | 85000  | 2    |

Both Akshay and John receive rank `1`.

---

## Step 4 — Filter Highest Paid Employees

```sql
WHERE rnk = 1
```

Returns only highest-paid employees from each department.

---

# Output

| department  | employee_name | salary |
| ----------- | ------------- | ------ |
| Engineering | Akshay        | 95000  |
| Engineering | John          | 95000  |
| HR          | Sneha         | 70000  |
| HR          | Meera         | 70000  |
| Finance     | Kiran         | 90000  |

---

# Why `DENSE_RANK()` Instead of `ROW_NUMBER()`?

## `ROW_NUMBER()`

Would return only one employee even if multiple employees share the highest salary.

Example:

| employee_name | salary | row_number |
| ------------- | ------ | ---------- |
| Akshay        | 95000  | 1          |
| John          | 95000  | 2          |

John would be excluded.

---

## `DENSE_RANK()`

Assigns the same rank for equal salaries.

Example:

| employee_name | salary | dense_rank |
| ------------- | ------ | ---------- |
| Akshay        | 95000  | 1          |
| John          | 95000  | 1          |

Both employees are returned.

---

# Alternative Approach Using Subquery

```sql
SELECT
    department,
    employee_name,
    salary
FROM Employee e
WHERE salary = (
    SELECT MAX(salary)
    FROM Employee
    WHERE department = e.department
);
```

---

# Which Approach is Better?

## `DENSE_RANK()`

- More scalable
- Cleaner for ranking problems
- Easily extendable to:
  - Top 3 salaries
  - Second highest salary
  - Department-wise ranking

## Correlated Subquery

- Simpler logic
- Good for beginners
- Can be slower on large datasets

---

# Follow-Up Variations

## 1. Second Highest Salary Per Department

```sql
WHERE rnk = 2
```

---

## 2. Top 3 Salaries Per Department

```sql
WHERE rnk <= 3
```

---

## 3. Lowest Paid Employee Per Department

```sql
DENSE_RANK() OVER (
    PARTITION BY department
    ORDER BY salary ASC
)
```

---

# Important Interview Concept

## `PARTITION BY`

```sql
PARTITION BY department
```

Creates separate ranking groups for each department.

Without `PARTITION BY`,
ranking happens across the entire table.
