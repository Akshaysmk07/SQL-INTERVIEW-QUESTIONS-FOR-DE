# Find First Order Date for Every Customer — MySQL Solution

## Approach 1: Using `MIN()`

### Query

```sql
SELECT
    customer_id,
    MIN(order_date) AS first_order_date
FROM Orders
GROUP BY customer_id
ORDER BY customer_id;
```

---

# Explanation

## Step 1 — Group Orders by Customer

```sql
GROUP BY customer_id
```

Creates one group for each customer.

Example:

### Customer 1

| Order Date |
| ---------- |
| 2025-01-10 |
| 2025-02-05 |
| 2025-01-05 |

---

## Step 2 — Find Earliest Date

```sql
MIN(order_date)
```

Returns the smallest (earliest) date within each customer group.

---

## Step 3 — Sort by Customer

```sql
ORDER BY customer_id
```

Displays results in ascending customer order.

---

# Output

| customer_id | first_order_date |
| ----------- | ---------------- |
| 1           | 2025-01-05       |
| 2           | 2025-01-12       |
| 3           | 2025-01-15       |

---

# Customer-Wise Calculation

## Customer 1

| Order Date |
| ---------- |
| 2025-01-10 |
| 2025-02-05 |
| 2025-01-05 |

Earliest:

```text
2025-01-05
```

---

## Customer 2

| Order Date |
| ---------- |
| 2025-01-12 |
| 2025-03-20 |

Earliest:

```text
2025-01-12
```

---

## Customer 3

| Order Date |
| ---------- |
| 2025-01-15 |
| 2025-02-10 |

Earliest:

```text
2025-01-15
```

---

# Approach 2: Using `ROW_NUMBER()`

Useful when you need additional columns from the first order.

### Query

```sql
SELECT
    customer_id,
    order_date AS first_order_date
FROM (
    SELECT
        customer_id,
        order_date,
        ROW_NUMBER() OVER (
            PARTITION BY customer_id
            ORDER BY order_date
        ) AS rn
    FROM Orders
) t
WHERE rn = 1
ORDER BY customer_id;
```

---

# Why Use `ROW_NUMBER()`?

Suppose the interviewer asks:

> Find the first order date and the corresponding order amount.

`MIN(order_date)` alone cannot directly return the associated amount.

Window functions solve that easily.

Example:

```sql
SELECT
    customer_id,
    order_date,
    order_amount
FROM (
    SELECT *,
           ROW_NUMBER() OVER (
               PARTITION BY customer_id
               ORDER BY order_date
           ) rn
    FROM Orders
) t
WHERE rn = 1;
```

---

# Follow-Up Variations

## 1. Last Order Date

```sql
SELECT
    customer_id,
    MAX(order_date) AS last_order_date
FROM Orders
GROUP BY customer_id;
```

---

## 2. First Order Amount

```sql
SELECT
    customer_id,
    order_amount
FROM (
    SELECT *,
           ROW_NUMBER() OVER (
               PARTITION BY customer_id
               ORDER BY order_date
           ) rn
    FROM Orders
) t
WHERE rn = 1;
```

---

## 3. Customers Whose First Order Exceeded 5000

```sql
SELECT *
FROM (
    SELECT *,
           ROW_NUMBER() OVER (
               PARTITION BY customer_id
               ORDER BY order_date
           ) rn
    FROM Orders
) t
WHERE rn = 1
  AND order_amount > 5000;
```

---

## 4. Days Since First Order

```sql
SELECT
    customer_id,
    DATEDIFF(
        CURDATE(),
        MIN(order_date)
    ) AS days_since_first_order
FROM Orders
GROUP BY customer_id;
```

---

## 5. First and Last Order Dates Together

```sql
SELECT
    customer_id,
    MIN(order_date) AS first_order_date,
    MAX(order_date) AS last_order_date
FROM Orders
GROUP BY customer_id;
```

---

# Interview Tip

Use:

| Requirement        | Best Function                      |
| ------------------ | ---------------------------------- |
| Earliest date only | `MIN()`                          |
| Latest date only   | `MAX()`                          |
| Entire first row   | `ROW_NUMBER()`                   |
| Entire last row    | `ROW_NUMBER() ORDER BY ... DESC` |

For this exact problem, the simplest and most efficient solution is:

```sql
SELECT
    customer_id,
    MIN(order_date) AS first_order_date
FROM Orders
GROUP BY customer_id;
```

However, interviewers often extend this into:

> "Now also return the first order amount."

At that point, switch to the `ROW_NUMBER()` approach.
