# Second Highest Salary — SQL Solutions

## Approach 1: Using `MAX()`

### Query

```sql
SELECT MAX(salary) AS SecondHighestSalary
FROM Employee
WHERE salary < (
    SELECT MAX(salary)
    FROM Employee
);
```

### Explanation

- First, find the highest salary using the inner query.
- Then, find the maximum salary smaller than the highest salary.
- This automatically ignores duplicate highest salaries.

### Example

| salary |
| ------ |
| 120000 |
| 120000 |
| 90000  |
| 70000  |

- Highest salary = `120000`
- Salaries less than highest = `90000, 70000`
- Maximum among them = `90000`

### Time Complexity

- Efficient for finding only the second highest salary.

---

# Approach 2: Using `DENSE_RANK()`

### Query

```sql
SELECT salary AS SecondHighestSalary
FROM (
    SELECT salary,
           DENSE_RANK() OVER (ORDER BY salary DESC) AS rnk
    FROM Employee
) t
WHERE rnk = 2;
```

### Explanation

- `DENSE_RANK()` assigns ranks to distinct salaries.
- Same salaries receive the same rank.
- The second highest distinct salary gets rank `2`.

### Ranking Example

| salary | rank |
| ------ | ---- |
| 120000 | 1    |
| 120000 | 1    |
| 90000  | 2    |
| 70000  | 3    |

Result:

```text
90000
```

### Advantages

- Easily extendable to:
  - 3rd highest salary
  - Nth highest salary
  - Top K salaries

---

# Key Interview Point

## Incorrect Approach

```sql
SELECT salary
FROM Employee
ORDER BY salary DESC
LIMIT 1 OFFSET 1;
```

### Why Wrong?

Because duplicates can return the same highest salary again.

Example:

| salary |
| ------ |
| 120000 |
| 120000 |
| 90000  |

Output becomes:

```text
120000
```

instead of:

```text
90000
```

Always use:

- `DISTINCT`
- `DENSE_RANK()`
- or comparison with `MAX()`

to correctly handle duplicates.
