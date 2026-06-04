# Find Previous Order Amount Using `LAG()` — MySQL Solution

## Approach: Using `LAG()`

### Query

```sql
SELECT
    customer_id,
    order_id,
    order_date,
    order_amount,
    LAG(order_amount) OVER (
        PARTITION BY customer_id
        ORDER BY order_date
    ) AS previous_order_amount
FROM Orders
ORDER BY customer_id, order_date;
```

---

# Explanation

## Step 1 — Partition by Customer

```sql
PARTITION BY customer_id
```

Creates separate windows for each customer.

Example:

### Customer 1

| Order |
| ----- |
| 101   |
| 102   |
| 103   |

### Customer 2

| Order |
| ----- |
| 104   |
| 105   |

---

## Step 2 — Sort Orders Chronologically

```sql
ORDER BY order_date
```

Ensures orders are processed in the sequence they were placed.

---

## Step 3 — Get Previous Order Amount

```sql
LAG(order_amount)
```

Returns the value from the previous row within the same customer partition.

If no previous row exists, `NULL` is returned automatically.

---

# Output

| customer_id | order_id | order_date | order_amount | previous_order_amount |
| ----------- | -------- | ---------- | ------------ | --------------------- |
| 1           | 101      | 2025-01-05 | 5000         | NULL                  |
| 1           | 102      | 2025-01-15 | 7000         | 5000                  |
| 1           | 103      | 2025-02-10 | 6500         | 7000                  |
| 2           | 104      | 2025-01-12 | 4000         | NULL                  |
| 2           | 105      | 2025-03-01 | 8000         | 4000                  |
| 3           | 106      | 2025-02-20 | 5500         | NULL                  |

---

# How `LAG()` Works

## Customer 1

| Order | Amount | Previous Amount |
| ----- | ------ | --------------- |
| 101   | 5000   | NULL            |
| 102   | 7000   | 5000            |
| 103   | 6500   | 7000            |

---

## Customer 2

| Order | Amount | Previous Amount |
| ----- | ------ | --------------- |
| 104   | 4000   | NULL            |
| 105   | 8000   | 4000            |

---

## Customer 3

| Order | Amount | Previous Amount |
| ----- | ------ | --------------- |
| 106   | 5500   | NULL            |

---

# Syntax

```sql
LAG(column_name, offset, default_value)
OVER (
    PARTITION BY ...
    ORDER BY ...
)
```

- `column_name` → Value to retrieve.
- `offset` → Number of rows back (default = 1).
- `default_value` → Returned if no previous row exists (default = NULL).

Example:

```sql
LAG(order_amount, 2, 0)
```

Returns the amount from two previous orders.
If unavailable, returns `0`.

---

# Follow-Up Variations

## 1. Find Next Order Amount (`LEAD()`)

```sql
SELECT
    customer_id,
    order_id,
    order_amount,
    LEAD(order_amount) OVER (
        PARTITION BY customer_id
        ORDER BY order_date
    ) AS next_order_amount
FROM Orders;
```

---

## 2. Difference Between Current and Previous Order

```sql
SELECT
    customer_id,
    order_id,
    order_amount,
    order_amount -
    LAG(order_amount) OVER (
        PARTITION BY customer_id
        ORDER BY order_date
    ) AS amount_difference
FROM Orders;
```

---

## 3. Percentage Change from Previous Order

```sql
SELECT
    customer_id,
    order_id,
    order_amount,
    ROUND(
        (
            order_amount -
            LAG(order_amount) OVER (
                PARTITION BY customer_id
                ORDER BY order_date
            )
        ) * 100.0 /
        LAG(order_amount) OVER (
            PARTITION BY customer_id
            ORDER BY order_date
        ),
        2
    ) AS percentage_change
FROM Orders;
```

---

## 4. Rank Orders by Amount

```sql
SELECT
    customer_id,
    order_id,
    order_amount,
    RANK() OVER (
        PARTITION BY customer_id
        ORDER BY order_amount DESC
    ) AS rank
FROM Orders;
```

---

# Interview Tip

Remember the three navigation functions:

| Function          | Purpose               |
| ----------------- | --------------------- |
| `LAG()`         | Previous row          |
| `LEAD()`        | Next row              |
| `FIRST_VALUE()` | First value in window |
| `LAST_VALUE()`  | Last value in window  |

A common interview pattern is:

```sql
LAG(column)
OVER (
    PARTITION BY group_column
    ORDER BY sequence_column
)
```

where:

- `PARTITION BY` defines the group.
- `ORDER BY` defines the sequence.
- `LAG()` retrieves the previous row's value.
