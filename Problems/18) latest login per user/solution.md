# Find Latest Login Per User — MySQL Solution

## Approach 1: Using `MAX()`

### Query

```sql
SELECT
    user_id,
    MAX(login_datetime) AS latest_login
FROM Logins
GROUP BY user_id
ORDER BY user_id;
```

---

# Explanation

## Step 1 — Group Logins by User

```sql
GROUP BY user_id
```

Creates one group for each user.

Example:

### User 101

| Login Time          |
| ------------------- |
| 2025-01-05 09:15:00 |
| 2025-01-10 08:45:00 |
| 2025-01-12 11:00:00 |

---

## Step 2 — Find Latest Login

```sql
MAX(login_datetime)
```

Returns the most recent login timestamp for each user.

---

## Step 3 — Sort Results

```sql
ORDER BY user_id
```

Displays users in ascending order.

---

# Output

| user_id | latest_login        |
| ------- | ------------------- |
| 101     | 2025-01-12 11:00:00 |
| 102     | 2025-01-15 16:10:00 |
| 103     | 2025-01-20 18:30:00 |

---

# User-Wise Calculation

## User 101

| Login               |
| ------------------- |
| 2025-01-05 09:15:00 |
| 2025-01-10 08:45:00 |
| 2025-01-12 11:00:00 |

Latest:

```text
2025-01-12 11:00:00
```

---

## User 102

Latest:

```text
2025-01-15 16:10:00
```

---

## User 103

Latest:

```text
2025-01-20 18:30:00
```

---

# Approach 2: Using `ROW_NUMBER()`

Useful when you need additional columns from the latest login row.

### Query

```sql
SELECT
    user_id,
    login_datetime AS latest_login
FROM (
    SELECT
        user_id,
        login_datetime,
        ROW_NUMBER() OVER (
            PARTITION BY user_id
            ORDER BY login_datetime DESC
        ) AS rn
    FROM Logins
) t
WHERE rn = 1
ORDER BY user_id;
```

---

# Why Use `ROW_NUMBER()`?

Suppose the interviewer asks:

> Return the latest login along with its `login_id`.

Then `MAX()` alone cannot directly return the associated `login_id`.

Example:

```sql
SELECT
    user_id,
    login_id,
    login_datetime
FROM (
    SELECT *,
           ROW_NUMBER() OVER (
               PARTITION BY user_id
               ORDER BY login_datetime DESC
           ) rn
    FROM Logins
) t
WHERE rn = 1;
```

---

# Follow-Up Variations

## 1. First Login Per User

```sql
SELECT
    user_id,
    MIN(login_datetime) AS first_login
FROM Logins
GROUP BY user_id;
```

---

## 2. Users Who Logged In More Than Once

```sql
SELECT
    user_id,
    COUNT(*) AS login_count
FROM Logins
GROUP BY user_id
HAVING COUNT(*) > 1;
```

---

## 3. Previous Login Time

```sql
SELECT
    user_id,
    login_datetime,
    LAG(login_datetime) OVER (
        PARTITION BY user_id
        ORDER BY login_datetime
    ) AS previous_login
FROM Logins;
```

---

## 4. Users Not Logged In During Last 30 Days

```sql
SELECT
    user_id,
    MAX(login_datetime) AS latest_login
FROM Logins
GROUP BY user_id
HAVING MAX(login_datetime) <
       CURDATE() - INTERVAL 30 DAY;
```

---

## 5. Latest Login and Total Logins

```sql
SELECT
    user_id,
    MAX(login_datetime) AS latest_login,
    COUNT(*) AS total_logins
FROM Logins
GROUP BY user_id;
```

---

# Interview Tip

Use:

| Requirement         | Best Function    |
| ------------------- | ---------------- |
| Earliest datetime   | `MIN()`        |
| Latest datetime     | `MAX()`        |
| Complete latest row | `ROW_NUMBER()` |
| Previous login      | `LAG()`        |
| Next login          | `LEAD()`       |

For this exact problem, the simplest and most efficient solution is:

```sql
SELECT
    user_id,
    MAX(login_datetime) AS latest_login
FROM Logins
GROUP BY user_id;
```

If the interviewer later asks for additional columns from the latest login record, switch to the `ROW_NUMBER()` approach.
