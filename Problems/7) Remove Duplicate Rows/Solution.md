# Remove Duplicate Rows — SQL Solution

## Correct Approach Using `ROW_NUMBER()`

### Query

```sql
DELETE FROM Users
WHERE id IN (
    SELECT id
    FROM (
        SELECT id,
               ROW_NUMBER() OVER (
                   PARTITION BY email
                   ORDER BY id
               ) AS rnk
        FROM Users
    ) t
    WHERE rnk > 1
);
```

---

# Explanation

## Step 1 — Partition Rows by Email

```sql
PARTITION BY email
```

Groups rows having the same email.

---

## Step 2 — Assign Row Numbers

```sql
ROW_NUMBER() OVER (
    PARTITION BY email
    ORDER BY id
)
```

Assigns:

| id | email            | row_number |
| -- | ---------------- | ---------- |
| 1  | akshay@gmail.com | 1          |
| 6  | akshay@gmail.com | 2          |

Smallest `id` gets `1`.

---

## Step 3 — Keep First Row

```sql
WHERE rnk > 1
```

Deletes:

- second duplicate
- third duplicate
- fourth duplicate
- etc.

Keeps only the smallest `id`.

---

# Why `ROW_NUMBER()` Instead of `DENSE_RANK()`?

## `ROW_NUMBER()`

Always gives unique sequence numbers:

| id | row_number |
| -- | ---------- |
| 1  | 1          |
| 6  | 2          |
| 9  | 3          |

Perfect for duplicate removal.

---

## `DENSE_RANK()`

Used for ranking distinct values.

Not ideal for deleting duplicates.

---

# Alternative Interview-Famous Solution

```sql
DELETE u1
FROM Users u1
JOIN Users u2
ON u1.email = u2.email
AND u1.id > u2.id;
```

---

# How It Works

If two rows have same email:

| id |
| -- |
| 1  |
| 6  |

Condition:

```sql
u1.id > u2.id
```

Deletes the larger `id`.

Keeps smallest `id`.

---

# Which Approach is Better?

## Self Join

- Classic SQL interview solution
- Very common in LeetCode

## Window Function

- Cleaner
- Easier to extend
- Modern SQL approach

---

# Follow-Up Variations

## Keep Latest Row Instead of Smallest ID

```sql
ORDER BY id DESC
```

---

## Remove Duplicates Based on Multiple Columns

```sql
PARTITION BY email, phone_number
```

---

## Count Duplicate Rows

```sql
SELECT email,
       COUNT(*) - 1 AS duplicates_removed
FROM Users
GROUP BY email
HAVING COUNT(*) > 1;
```
