# Employees Joined in Last 30 Days — Oracle SQL Solution

## Approach Using `SYSDATE`

### Query

```sql
SELECT
    employee_id,
    employee_name,
    department,
    join_date
FROM employees
WHERE join_date > SYSDATE - 30
ORDER BY join_date DESC;
```

---

# Explanation

## Step 1 — Get Current System Date

```sql
SYSDATE
```

Returns the current Oracle database date and time.

Example:

```text
2026-05-22
```

---

## Step 2 — Subtract 30 Days

```sql
SYSDATE - 30
```

Oracle allows direct date arithmetic.

Example:

```text
Current Date: 2026-05-22
SYSDATE - 30 → 2026-04-22
```

---

## Step 3 — Filter Recent Employees

```sql
WHERE join_date > SYSDATE - 30
```

Returns employees who joined within the last 30 days.

---

## Step 4 — Sort Latest Joiners First

```sql
ORDER BY join_date DESC
```

Displays newest employees at the top.

---

# Output

| EMPLOYEE_ID | EMPLOYEE_NAME | DEPARTMENT  | JOIN_DATE   |
| ----------- | ------------- | ----------- | ----------- |
| 1           | Akshay        | Engineering | Recent Date |
| 2           | Rahul         | Finance     | Recent Date |
| 4           | Kiran         | Engineering | Recent Date |

---

# Why Oracle Date Arithmetic Works?

In Oracle:

```sql
DATE - NUMBER
```

means subtracting days.

Example:

```sql
SYSDATE - 7
```

→ last 7 days

```sql
SYSDATE - 30
```

→ last 30 days

---

# Follow-Up Variations

## 1. Employees Joined in Last 7 Days

```sql
SELECT *
FROM employees
WHERE join_date > SYSDATE - 7;
```

---

## 2. Employees Joined in Current Month

```sql
SELECT *
FROM employees
WHERE TRUNC(join_date, 'MM') = TRUNC(SYSDATE, 'MM');
```

---

# Explanation

```sql
TRUNC(date, 'MM')
```

Converts date to first day of the month.

Example:

| Original Date | Truncated  |
| ------------- | ---------- |
| 2026-05-18    | 2026-05-01 |

Useful for month-based filtering.

---

## 3. Employees Joined Between Two Dates

```sql
SELECT *
FROM employees
WHERE join_date BETWEEN
    TO_DATE('2026-01-01', 'YYYY-MM-DD')
AND TO_DATE('2026-03-31', 'YYYY-MM-DD');
```

---

## 4. Employees Who Completed 1 Year

```sql
SELECT *
FROM employees
WHERE join_date <= ADD_MONTHS(SYSDATE, -12);
```

---

# Important Oracle Interview Concepts

## `SYSDATE`

Returns current database date and time.

---

## `TRUNC()`

Removes time portion from dates.

---

## `ADD_MONTHS()`

Adds or subtracts months from a date.

Example:

```sql
ADD_MONTHS(SYSDATE, -12)
```

→ one year ago
