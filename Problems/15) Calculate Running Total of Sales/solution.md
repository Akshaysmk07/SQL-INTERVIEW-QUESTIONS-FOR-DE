# Calculate Running Total of Sales — MySQL Solution

## Approach: Using Window Function `SUM() OVER()`

### Query

```sql
SELECT
    sale_id,
    sale_date,
    sales_amount,
    SUM(sales_amount) OVER (
        ORDER BY sale_date
    ) AS running_total
FROM Sales
ORDER BY sale_date;
```

---

# Explanation

## Step 1 — Sort Sales by Date

```sql
ORDER BY sale_date
```

Processes sales chronologically.

| Sale Date  | Amount |
| ---------- | ------ |
| 2025-01-05 | 5000   |
| 2025-01-10 | 7000   |
| 2025-01-15 | 3000   |
| 2025-01-20 | 6000   |
| 2025-01-25 | 4000   |

---

## Step 2 — Calculate Running Total

```sql
SUM(sales_amount)
OVER (ORDER BY sale_date)
```

Continuously adds the current row's amount to all previous rows.

---

# Running Total Calculation

| Sale Date  | Amount | Running Total |
| ---------- | ------ | ------------- |
| 2025-01-05 | 5000   | 5000          |
| 2025-01-10 | 7000   | 12000         |
| 2025-01-15 | 3000   | 15000         |
| 2025-01-20 | 6000   | 21000         |
| 2025-01-25 | 4000   | 25000         |

---

# Output

| sale_id | sale_date  | sales_amount | running_total |
| ------- | ---------- | ------------ | ------------- |
| 1       | 2025-01-05 | 5000         | 5000          |
| 2       | 2025-01-10 | 7000         | 12000         |
| 3       | 2025-01-15 | 3000         | 15000         |
| 4       | 2025-01-20 | 6000         | 21000         |
| 5       | 2025-01-25 | 4000         | 25000         |

---

# How `SUM() OVER()` Works

The window expands row by row:

| Rows Included                    | Sum   |
| -------------------------------- | ----- |
| 5000                             | 5000  |
| 5000 + 7000                      | 12000 |
| 5000 + 7000 + 3000               | 15000 |
| 5000 + 7000 + 3000 + 6000        | 21000 |
| 5000 + 7000 + 3000 + 6000 + 4000 | 25000 |

---

# Equivalent Explicit Syntax

```sql
SELECT
    sale_id,
    sale_date,
    sales_amount,
    SUM(sales_amount) OVER (
        ORDER BY sale_date
        ROWS BETWEEN UNBOUNDED PRECEDING
        AND CURRENT ROW
    ) AS running_total
FROM Sales;
```

### Meaning

```text
UNBOUNDED PRECEDING
```

→ Start from the first row.

```text
CURRENT ROW
```

→ End at the current row.

---

# Follow-Up Variations

## 1. Running Total Per Product

```sql
SELECT
    product_name,
    sale_date,
    sales_amount,
    SUM(sales_amount) OVER (
        PARTITION BY product_name
        ORDER BY sale_date
    ) AS running_total
FROM Sales;
```

---

## 2. Cumulative Average Sales

```sql
SELECT
    sale_id,
    sale_date,
    sales_amount,
    AVG(sales_amount) OVER (
        ORDER BY sale_date
    ) AS running_average
FROM Sales;
```

---

## 3. First Date Cumulative Sales Exceeded 50000

```sql
SELECT *
FROM (
    SELECT
        sale_date,
        SUM(sales_amount) OVER (
            ORDER BY sale_date
        ) AS running_total
    FROM Sales
) t
WHERE running_total > 50000
LIMIT 1;
```

---

## 4. Running Total Month-Wise

```sql
SELECT
    sale_date,
    sales_amount,
    SUM(sales_amount) OVER (
        PARTITION BY YEAR(sale_date),
                     MONTH(sale_date)
        ORDER BY sale_date
    ) AS monthly_running_total
FROM Sales;
```

---

## 5. Running Total Without Window Functions (Self Join)

```sql
SELECT
    s1.sale_id,
    s1.sale_date,
    s1.sales_amount,
    SUM(s2.sales_amount) AS running_total
FROM Sales s1
JOIN Sales s2
ON s2.sale_date <= s1.sale_date
GROUP BY
    s1.sale_id,
    s1.sale_date,
    s1.sales_amount
ORDER BY s1.sale_date;
```

---

# Interview Tip

The three most common window-function aggregates are:

| Requirement     | Function           |
| --------------- | ------------------ |
| Running Total   | `SUM() OVER()`   |
| Running Average | `AVG() OVER()`   |
| Running Count   | `COUNT() OVER()` |

A running total question almost always uses:

```sql
SUM(column_name)
OVER (
    ORDER BY some_column
)
```

For partition-wise cumulative totals, simply add:

```sql
PARTITION BY group_column
```

before the `ORDER BY`.
