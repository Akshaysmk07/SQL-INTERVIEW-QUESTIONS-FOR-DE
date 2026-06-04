# Find Consecutive Login Days — MySQL Solution

## Approach: Using `LAG()`

### Query

```sql
SELECT
    user_id,
    login_date,
    previous_login_date
FROM (
    SELECT
        user_id,
        login_date,
        LAG(login_date) OVER (
            PARTITION BY user_id
            ORDER BY login_date
        ) AS previous_login_date
    FROM Logins
) t
WHERE DATEDIFF(login_date, previous_login_date) = 1
ORDER BY user_id, login_date;
```

---

# Explanation

## Step 1 — Partition by User

```sql
PARTITION BY user_id
```

Creates separate login histories for each user.

Example:

### User 101

| Login Date |
| ---------- |
| 2025-01-01 |
| 2025-01-02 |
| 2025-01-04 |

---

## Step 2 — Get Previous Login Date

```sql
LAG(login_date)
```

Returns the previous login date for the same user.

Result:

| Login Date | Previous Login |
| ---------- | -------------- |
| 2025-01-01 | NULL           |
| 2025-01-02 | 2025-01-01     |
| 2025-01-04 | 2025-01-02     |

---

## Step 3 — Calculate Day Difference

```sql
DATEDIFF(login_date, previous_login_date)
```

Returns:

| Current    | Previous   | Difference |
| ---------- | ---------- | ---------- |
| 2025-01-02 | 2025-01-01 | 1          |
| 2025-01-04 | 2025-01-02 | 2          |

---

## Step 4 — Keep Consecutive Logins

```sql
WHERE DATEDIFF(...) = 1
```

Keeps only logins exactly one day apart.

---

# Output

| user_id | login_date | previous_login_date |
| ------- | ---------- | ------------------- |
| 101     | 2025-01-02 | 2025-01-01          |
| 102     | 2025-01-06 | 2025-01-05          |
| 102     | 2025-01-07 | 2025-01-06          |

---

# How `LAG()` Works

## User 101

| Login      | Previous   | Difference |
| ---------- | ---------- | ---------- |
| 2025-01-01 | NULL       | -          |
| 2025-01-02 | 2025-01-01 | 1 ✅       |
| 2025-01-04 | 2025-01-02 | 2 ❌       |

---

## User 102

| Login      | Previous   | Difference |
| ---------- | ---------- | ---------- |
| 2025-01-05 | NULL       | -          |
| 2025-01-06 | 2025-01-05 | 1 ✅       |
| 2025-01-07 | 2025-01-06 | 1 ✅       |

---

## User 103

| Login      | Previous   | Difference |
| ---------- | ---------- | ---------- |
| 2025-01-03 | NULL       | -          |
| 2025-01-05 | 2025-01-03 | 2 ❌       |

---

# Follow-Up Variations

## 1. Find Login Gaps

```sql
SELECT
    user_id,
    login_date,
    previous_login_date,
    DATEDIFF(
        login_date,
        previous_login_date
    ) AS gap_days
FROM (
    SELECT
        user_id,
        login_date,
        LAG(login_date) OVER (
            PARTITION BY user_id
            ORDER BY login_date
        ) AS previous_login_date
    FROM Logins
) t;
```

---

## 2. Users Whose Latest Two Logins Were Consecutive

```sql
SELECT *
FROM (
    SELECT
        user_id,
        login_date,
        LAG(login_date) OVER (
            PARTITION BY user_id
            ORDER BY login_date
        ) AS previous_login_date,
        ROW_NUMBER() OVER (
            PARTITION BY user_id
            ORDER BY login_date DESC
        ) AS rn
    FROM Logins
) t
WHERE rn = 1
AND DATEDIFF(
        login_date,
        previous_login_date
    ) = 1;
```

---

## 3. Find Next Login Date (`LEAD()`)

```sql
SELECT
    user_id,
    login_date,
    LEAD(login_date) OVER (
        PARTITION BY user_id
        ORDER BY login_date
    ) AS next_login
FROM Logins;
```

---

## 4. Find Users with 3 Consecutive Login Days

```sql
SELECT *
FROM (
    SELECT
        user_id,
        login_date,
        LAG(login_date, 1) OVER (
            PARTITION BY user_id
            ORDER BY login_date
        ) AS prev1,
        LAG(login_date, 2) OVER (
            PARTITION BY user_id
            ORDER BY login_date
        ) AS prev2
    FROM Logins
) t
WHERE DATEDIFF(login_date, prev1) = 1
AND DATEDIFF(prev1, prev2) = 1;
```

---

# Interview Tip

This is a classic **Window Function + Date Function** problem.

The common pattern is:

```sql
LAG(date_column)
OVER (
    PARTITION BY group_column
    ORDER BY date_column
)
```

Then compare using:

```sql
DATEDIFF(
    current_date,
    previous_date
)
```

Remember:

| Requirement         | Function                   |
| ------------------- | -------------------------- |
| Previous row        | `LAG()`                  |
| Next row            | `LEAD()`                 |
| Date gap            | `DATEDIFF()`             |
| Consecutive records | `LAG()` + `DATEDIFF()` |

This combination appears very frequently in MySQL and Data Engineer interviews.
