# Find Duplicate Emails — SQL Solution

## Approach 1: Using `GROUP BY` + `HAVING`

### Query

```sql
SELECT email
FROM Users
GROUP BY email
HAVING COUNT(*) > 1;
```

---

## Explanation

### Step 1 — Group Emails

```sql
GROUP BY email
```

Groups all identical emails together.

---

### Step 2 — Count Occurrences

```sql
COUNT(*)
```

Counts how many times each email appears.

---

### Step 3 — Filter Duplicate Emails

```sql
HAVING COUNT(*) > 1
```

Returns only emails appearing more than once.

---

# Example

## Input

| id | name   | email            |
| -- | ------ | ---------------- |
| 1  | Akshay | akshay@gmail.com |
| 2  | Rahul  | rahul@gmail.com  |
| 3  | Sneha  | sneha@gmail.com  |
| 4  | Kiran  | rahul@gmail.com  |
| 5  | Meera  | meera@gmail.com  |
| 6  | John   | akshay@gmail.com |

---

## Grouped Result

| email            | count |
| ---------------- | ----- |
| akshay@gmail.com | 2     |
| rahul@gmail.com  | 2     |
| sneha@gmail.com  | 1     |

---

## Final Output

| email            |
| ---------------- |
| akshay@gmail.com |
| rahul@gmail.com  |

---

# Approach 2: Using Self Join

### Query

```sql
SELECT DISTINCT u1.email
FROM Users u1
JOIN Users u2
ON u1.email = u2.email
AND u1.id <> u2.id;
```

---

# Explanation

- Join the table with itself.
- Match rows having the same email.
- Ensure different rows using:

```sql
u1.id <> u2.id
```

- `DISTINCT` removes repeated output emails.

---

# How Self Join Works

Example:

| u1.id | u2.id | email            |
| ----- | ----- | ---------------- |
| 1     | 6     | akshay@gmail.com |
| 6     | 1     | akshay@gmail.com |
| 2     | 4     | rahul@gmail.com  |
| 4     | 2     | rahul@gmail.com  |

Using `DISTINCT` gives:

```text
akshay@gmail.com
rahul@gmail.com
```

---

# Best Approach for Interviews

## Recommended

```sql
GROUP BY + HAVING
```

because:

- Cleaner
- More readable
- Better performance
- Standard SQL duplicate detection pattern

---

# Follow-Up Variations

## 1. Count Duplicate Occurrences

```sql
SELECT email,
       COUNT(*) AS duplicate_count
FROM Users
GROUP BY email
HAVING COUNT(*) > 1;
```

---

## 2. Delete Duplicate Rows While Keeping One Record

```sql
DELETE u1
FROM Users u1
JOIN Users u2
ON u1.email = u2.email
AND u1.id > u2.id;
```

Keeps the smallest `id` and removes duplicates.

---

# Key Interview Concept

## Difference Between `WHERE` and `HAVING`

- `WHERE`
  filters rows before grouping
- `HAVING`
  filters groups after aggregation

Since duplicates depend on:

```sql
COUNT(*)
```

we must use:

```sql
HAVING COUNT(*) > 1
```
