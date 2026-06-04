# Find 7-Day Moving Average of Sales — MySQL Solution

## Approach: Using `AVG() OVER()`

### Query

```sql
SELECT
    sale_date,
    sales_amount,
    ROUND(
        AVG(sales_amount) OVER (
            ORDER BY sale_date
            ROWS BETWEEN 6 PRECEDING
            AND CURRENT ROW
        ),
        2
    ) AS moving_avg_7_days
FROM Sales
ORDER BY sale_date;
```

---

# Explanation

## Step 1 — Sort Sales by Date

```sql
ORDER BY sale_date
```

Processes rows chronologically.

| Sale Date  | Amount |
| ---------- | ------ |
| 2025-01-01 | 100    |
| 2025-01-02 | 200    |
| 2025-01-03 | 300    |
| ...        | ...    |

---

## Step 2 — Define the Window Frame

```sql
ROWS BETWEEN 6 PRECEDING
AND CURRENT ROW
```

Means:

- Include the current row.
- Include up to 6 rows before it.

Maximum window size:

```text
7 rows
```

---

## Step 3 — Calculate Average

```sql
AVG(sales_amount)
```

Computes the average within the defined window.

---

## Step 4 — Round to Two Decimals

```sql
ROUND(..., 2)
```

Formats the moving average nicely.

---

# How the Window Moves

## Day 1

Window:

| Amount |
| ------ |
| 100    |

Average:

:contentReference[oaicite:0]{index=0}

---

## Day 2

Window:

| Amount |
| ------ |
| 100    |
| 200    |

Average:

:contentReference[oaicite:1]{index=1}

---

## Day 7

Window:

| Amount |
| ------ |
| 100    |
| 200    |
| 300    |
| 400    |
| 500    |
| 600    |
| 700    |

Average:

:contentReference[oaicite:2]{index=2}

---

## Day 8

Window:

| Amount |
| ------ |
| 200    |
| 300    |
| 400    |
| 500    |
| 600    |
| 700    |
| 800    |

Average:

:contentReference[oaicite:3]{index=3}

---

# Output

| sale_date  | sales_amount | moving_avg_7_days |
| ---------- | ------------ | ----------------- |
| 2025-01-01 | 100          | 100.00            |
| 2025-01-02 | 200          | 150.00            |
| 2025-01-03 | 300          | 200.00            |
| 2025-01-04 | 400          | 250.00            |
| 2025-01-05 | 500          | 300.00            |
| 2025-01-06 | 600          | 350.00            |
| 2025-01-07 | 700          | 400.00            |
| 2025-01-08 | 800          | 500.00            |
| 2025-01-09 | 900          | 600.00            |
| 2025-01-10 | 1000         | 700.00            |

---

# General Formula

For an N-day moving average:

```sql
AVG(column_name) OVER (
    ORDER BY date_column
    ROWS BETWEEN N-1 PRECEDING
    AND CURRENT ROW
)
```

Examples:

| Requirement    | Window Frame                                  |
| -------------- | --------------------------------------------- |
| 3-Day Average  | `ROWS BETWEEN 2 PRECEDING AND CURRENT ROW`  |
| 7-Day Average  | `ROWS BETWEEN 6 PRECEDING AND CURRENT ROW`  |
| 30-Day Average | `ROWS BETWEEN 29 PRECEDING AND CURRENT ROW` |

---

# Follow-Up Variations

## 1. 3-Day Moving Average

```sql
SELECT
    sale_date,
    sales_amount,
    AVG(sales_amount) OVER (
        ORDER BY sale_date
        ROWS BETWEEN 2 PRECEDING
        AND CURRENT ROW
    ) AS moving_avg_3_days
FROM Sales;
```

---

## 2. Moving Average Per Product

```sql
SELECT
    product_name,
    sale_date,
    sales_amount,
    AVG(sales_amount) OVER (
        PARTITION BY product_name
        ORDER BY sale_date
        ROWS BETWEEN 6 PRECEDING
        AND CURRENT ROW
    ) AS moving_avg
FROM Sales;
```

---

## 3. Highest 7-Day Moving Average

```sql
SELECT MAX(moving_avg_7_days)
FROM (
    SELECT
        AVG(sales_amount) OVER (
            ORDER BY sale_date
            ROWS BETWEEN 6 PRECEDING
            AND CURRENT ROW
        ) AS moving_avg_7_days
    FROM Sales
) t;
```

---

## 4. 30-Day Rolling Sum

```sql
SELECT
    sale_date,
    SUM(sales_amount) OVER (
        ORDER BY sale_date
        ROWS BETWEEN 29 PRECEDING
        AND CURRENT ROW
    ) AS rolling_sum
FROM Sales;
```

---

## 5. Compare Current Sales with Moving Average

```sql
SELECT
    sale_date,
    sales_amount,
    AVG(sales_amount) OVER (
        ORDER BY sale_date
        ROWS BETWEEN 6 PRECEDING
        AND CURRENT ROW
    ) AS moving_avg,
    sales_amount -
    AVG(sales_amount) OVER (
        ORDER BY sale_date
        ROWS BETWEEN 6 PRECEDING
        AND CURRENT ROW
    ) AS difference
FROM Sales;
```

---

# Interview Tip

Remember these common window aggregates:

| Requirement     | Function         |
| --------------- | ---------------- |
| Running Total   | `SUM() OVER()` |
| Running Average | `AVG() OVER()` |
| Previous Row    | `LAG()`        |
| Next Row        | `LEAD()`       |

A moving average problem almost always uses:

```sql
AVG(column)
OVER (
    ORDER BY date_column
    ROWS BETWEEN N PRECEDING
    AND CURRENT ROW
)
```

The key concept is the **window frame**:

```sql
ROWS BETWEEN 6 PRECEDING
AND CURRENT ROW
```

which defines exactly which rows participate in each calculation.
