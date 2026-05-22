# Monthly Sales Report — Oracle SQL Solution

## Approach: Using `TO_CHAR()` + `GROUP BY`

### Query

```sql
SELECT
    TO_CHAR(sale_date, 'YYYY-MM') AS month,
    SUM(amount) AS total_sales
FROM sales
GROUP BY TO_CHAR(sale_date, 'YYYY-MM')
ORDER BY TO_CHAR(sale_date, 'YYYY-MM');
```

---

# Explanation

## Step 1 — Convert Date to Month Format

```sql
TO_CHAR(sale_date, 'YYYY-MM')
```

Converts Oracle `DATE` values into:

```text
2025-01
2025-02
2025-03
```

This groups all sales belonging to the same month.

---

## Step 2 — Calculate Monthly Sales

```sql
SUM(amount)
```

Adds all sales amounts for each month.

---

## Step 3 — Group Records Month-Wise

```sql
GROUP BY TO_CHAR(sale_date, 'YYYY-MM')
```

Creates one group for each month.

---

## Step 4 — Sort Results

```sql
ORDER BY TO_CHAR(sale_date, 'YYYY-MM')
```

Returns months in ascending chronological order.

---

# Output

| MONTH   | TOTAL_SALES |
| ------- | ----------- |
| 2025-01 | 56200       |
| 2025-02 | 17500       |
| 2025-03 | 83500       |

---

# Month-Wise Calculation

## January 2025

| Product | Amount |
| ------- | ------ |
| Laptop  | 55000  |
| Mouse   | 1200   |

Total:

```text
56200
```

---

## February 2025

| Product  | Amount |
| -------- | ------ |
| Keyboard | 2500   |
| Monitor  | 15000  |

Total:

```text
17500
```

---

## March 2025

| Product | Amount |
| ------- | ------ |
| Laptop  | 60000  |
| Mouse   | 1500   |
| Tablet  | 22000  |

Total:

```text
83500
```

---

# Better Oracle Approach Using `TRUNC()`

In Oracle interviews, this is considered more efficient:

```sql
SELECT
    TO_CHAR(TRUNC(sale_date, 'MM'), 'YYYY-MM') AS month,
    SUM(amount) AS total_sales
FROM sales
GROUP BY TRUNC(sale_date, 'MM')
ORDER BY TRUNC(sale_date, 'MM');
```

---

# Why `TRUNC()` is Better?

```sql
TRUNC(sale_date, 'MM')
```

Converts all dates to the first day of the month.

Example:

| Original Date | Truncated Date |
| ------------- | -------------- |
| 2025-03-18    | 2025-03-01     |
| 2025-03-12    | 2025-03-01     |

This is:

- More efficient
- More Oracle-specific
- Better for indexing and optimization

---

# Follow-Up Variations

## 1. Highest Sales Month

```sql
SELECT *
FROM (
    SELECT
        TO_CHAR(sale_date, 'YYYY-MM') AS month,
        SUM(amount) AS total_sales
    FROM sales
    GROUP BY TO_CHAR(sale_date, 'YYYY-MM')
    ORDER BY total_sales DESC
)
WHERE ROWNUM = 1;
```

---

## 2. Average Monthly Sales

```sql
SELECT AVG(monthly_sales) AS avg_sales
FROM (
    SELECT SUM(amount) AS monthly_sales
    FROM sales
    GROUP BY TO_CHAR(sale_date, 'YYYY-MM')
);
```

---

## 3. Monthly Sales Per Product

```sql
SELECT
    TO_CHAR(sale_date, 'YYYY-MM') AS month,
    product_name,
    SUM(amount) AS total_sales
FROM sales
GROUP BY
    TO_CHAR(sale_date, 'YYYY-MM'),
    product_name
ORDER BY month;
```

---

# Important Oracle Interview Concept

## Difference Between `TO_CHAR()` and `TRUNC()`

### `TO_CHAR()`

Used for formatting display.

### `TRUNC()`

Used for actual date grouping and calculations.

Best practice:

- Group using `TRUNC()`
- Display using `TO_CHAR()`
