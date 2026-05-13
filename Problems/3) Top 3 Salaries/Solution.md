Your solution is correct and interview-ready.
Here’s a cleaner markdown-formatted version with explanation.

```md
# Top 3 Highest Distinct Salaries — SQL Solution

## Approach 1: Using `DENSE_RANK()`

### Query

```sql
SELECT DISTINCT salary
FROM (
    SELECT salary,
           DENSE_RANK() OVER (ORDER BY salary DESC) AS rnk
    FROM Employee
) tab
WHERE rnk <= 3;
```

---

# Explanation

## Step 1 — Rank Salaries

```sql
DENSE_RANK() OVER (ORDER BY salary DESC)
```

Assigns ranks to distinct salaries in descending order.

Example:

| salary | rank |
| ------ | ---- |
| 120000 | 1    |
| 120000 | 1    |
| 95000  | 2    |
| 90000  | 3    |
| 85000  | 4    |

---

## Step 2 — Filter Top 3 Ranks

```sql
WHERE rnk <= 3
```

Returns only:

- Rank 1
- Rank 2
- Rank 3

---

## Step 3 — Remove Duplicates

```sql
SELECT DISTINCT salary
```

Ensures duplicate salaries appear only once.

---

# Output

| salary |
| ------ |
| 120000 |
| 95000  |
| 90000  |

---

# Why `DENSE_RANK()`?

`DENSE_RANK()` handles duplicates properly.

Example:

| salary | rank |
| ------ | ---- |
| 120000 | 1    |
| 120000 | 1    |
| 95000  | 2    |
| 90000  | 3    |

No ranks are skipped.

---

# Important Interview Point

## Difference Between `RANK()` and `DENSE_RANK()`

### Using `RANK()`

| salary | rank |
| ------ | ---- |
| 120000 | 1    |
| 120000 | 1    |
| 95000  | 3    |

Rank `2` gets skipped.

---

### Using `DENSE_RANK()`

| salary | rank |
| ------ | ---- |
| 120000 | 1    |
| 120000 | 1    |
| 95000  | 2    |

No gaps in ranking.

---

# Alternative Approach Using `LIMIT`

```sql
SELECT DISTINCT salary
FROM Employee
ORDER BY salary DESC
LIMIT 3;
```

---

# Which Approach is Better?

## `LIMIT`

- Simple
- Shorter query
- Good for MySQL/PostgreSQL

## `DENSE_RANK()`

- More scalable
- Works for:
  - Top N salaries
  - Department-wise ranking
  - Employee ranking problems
- Common in product-company interviews

---

# Follow-Up Variations

## Top 5 Salaries

```sql
WHERE rnk <= 5
```

---

## Third Highest Salary

```sql
WHERE rnk = 3
```

---

## Employees Earning Top 3 Salaries

```sql
SELECT name, salary
FROM (
    SELECT name,
           salary,
           DENSE_RANK() OVER (ORDER BY salary DESC) AS rnk
    FROM Employee
) t
WHERE rnk <= 3;
```

```

```
