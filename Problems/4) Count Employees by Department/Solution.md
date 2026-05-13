# Count Employees by Department — SQL Solution

## Approach: Using `GROUP BY`

### Query

```sql
SELECT department,
       COUNT(*) AS employee_count
FROM Employee
GROUP BY department;
```

---

# Explanation

## Step 1 — Group Employees by Department

```sql
GROUP BY department
```

Groups all employees belonging to the same department together.

---

## Step 2 — Count Employees

```sql
COUNT(*)
```

Counts the number of rows (employees) in each department.

---

# Example

## Input

| id | name   | department  |
| -- | ------ | ----------- |
| 1  | Akshay | Engineering |
| 2  | Rahul  | Engineering |
| 3  | Sneha  | HR          |
| 4  | Kiran  | Finance     |
| 5  | Meera  | HR          |
| 6  | John   | Engineering |

---

## Grouped Result

| department  | employee_count |
| ----------- | -------------- |
| Engineering | 3              |
| HR          | 2              |
| Finance     | 1              |

---

# Output

| department  | employee_count |
| ----------- | -------------- |
| Engineering | 3              |
| HR          | 2              |
| Finance     | 2              |

---

# Why `COUNT(*)`?

```sql
COUNT(*)
```

counts all rows in each group.

Alternative:

```sql
COUNT(id)
```

also works because `id` is non-null.

---

# Follow-Up Variations

## 1. Departments Having More Than 2 Employees

```sql
SELECT department,
       COUNT(*) AS employee_count
FROM Employee
GROUP BY department
HAVING COUNT(*) > 2;
```

---

## 2. Average Salary by Department

```sql
SELECT department,
       AVG(salary) AS avg_salary
FROM Employee
GROUP BY department;
```

---

## 3. Highest Salary in Each Department

```sql
SELECT department,
       MAX(salary) AS highest_salary
FROM Employee
GROUP BY department;
```

---

## 4. Total Salary Expense by Department

```sql
SELECT department,
       SUM(salary) AS total_salary
FROM Employee
GROUP BY department;
```

---

# Important Interview Concept

## Difference Between `WHERE` and `HAVING`

### `WHERE`

Filters rows before grouping.

### `HAVING`

Filters groups after aggregation.

Example:

```sql
HAVING COUNT(*) > 2
```

filters departments after counting employees.
