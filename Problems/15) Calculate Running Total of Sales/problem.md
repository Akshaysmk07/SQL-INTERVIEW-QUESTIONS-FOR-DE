# Calculate Running Total of Sales — MySQL LeetCode Style Problem

## Problem Statement

Write a MySQL query to calculate the **running total (cumulative sum)** of sales amount ordered by sale date.

Return:

* Sale ID
* Sale Date
* Sales Amount
* Running Total

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
(1, '2025-01-05', 5000),
(2, '2025-01-10', 7000),
(3, '2025-01-15', 3000),
(4, '2025-01-20', 6000),
(5, '2025-01-25', 4000);
```

---

## Expected Output

| sale_id | sale_date  | sales_amount | running_total |
| ------- | ---------- | ------------ | ------------- |
| 1       | 2025-01-05 | 5000         | 5000          |
| 2       | 2025-01-10 | 7000         | 12000         |
| 3       | 2025-01-15 | 3000         | 15000         |
| 4       | 2025-01-20 | 6000         | 21000         |
| 5       | 2025-01-25 | 4000         | 25000         |

---

## Explanation

| Sale Date  | Amount | Running Total |
| ---------- | ------ | ------------- |
| 2025-01-05 | 5000   | 5000          |
| 2025-01-10 | 7000   | 12000         |
| 2025-01-15 | 3000   | 15000         |
| 2025-01-20 | 6000   | 21000         |
| 2025-01-25 | 4000   | 25000         |

The running total is calculated by continuously adding the current sale amount to the sum of all previous sales.

---

## Constraints

* `1 <= Sales rows <= 10^5`
* Sales amounts are positive integers.
* Sale dates are unique.
* Output should be sorted by `sale_date`.

---

## Follow-Up Variations

1. Calculate running total for each product separately.
2. Calculate running total month-wise.
3. Find the first date when cumulative sales exceeded 50,000.
4. Calculate cumulative average sales.
5. Calculate running total using a self join instead of window functions.
