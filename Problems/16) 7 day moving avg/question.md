# Find 7-Day Moving Average of Sales — MySQL LeetCode Style Problem

## Problem Statement

Write a MySQL query to calculate the **7-day moving average** of sales amounts.

For each sale date, compute the average sales amount considering the current day and the previous 6 days.

Return:

* Sale Date
* Sales Amount
* 7-Day Moving Average

Sort the output by `sale_date`.

---

## Table Schema

```sql
CREATE TABLE Sales (
    sale_id INT PRIMARY KEY,
    sale_date DATE,
    sales_amount INT
);
```

---

## Sample Data

```sql
INSERT INTO Sales (sale_id, sale_date, sales_amount) VALUES
(1, '2025-01-01', 100),
(2, '2025-01-02', 200),
(3, '2025-01-03', 300),
(4, '2025-01-04', 400),
(5, '2025-01-05', 500),
(6, '2025-01-06', 600),
(7, '2025-01-07', 700),
(8, '2025-01-08', 800),
(9, '2025-01-09', 900),
(10, '2025-01-10', 1000);
```

---

## Expected Output

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

## Explanation

For  **2025-01-07** :

Average of:

```
100 + 200 + 300 + 400 + 500 + 600 + 700
----------------------------------------- = 400
                    7
```

For  **2025-01-08** :

Average of:

```
200 + 300 + 400 + 500 + 600 + 700 + 800
----------------------------------------- = 500
                    7
```

The calculation always considers the current row and the previous six rows ordered by date.

---

## Constraints

* `1 <= Sales rows <= 10^5`
* Sales amounts are positive integers.
* Sale dates are unique.
* Output should be sorted by `sale_date`.

---

## Follow-Up Variations

1. Find the 3-day moving average.
2. Calculate moving average for each product separately.
3. Find the highest 7-day moving average.
4. Calculate a 30-day rolling sum.
5. Compare current sales with the 7-day moving average.
