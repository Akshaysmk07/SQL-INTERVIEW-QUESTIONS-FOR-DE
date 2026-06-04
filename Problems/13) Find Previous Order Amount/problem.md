# Find Previous Order Amount Using `LAG()` — MySQL LeetCode Style Problem

## Problem Statement

Write a MySQL query to display each order along with the amount of the **previous order** placed by the same customer.

Return:

* Customer ID
* Order ID
* Order Date
* Current Order Amount
* Previous Order Amount

If there is no previous order for a customer, return `NULL` for the previous order amount.

Sort the output by `customer_id` and `order_date`.

---

## Table Schema

```sql
CREATE TABLE Orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE,
    order_amount INT
);
```

---

## Sample Data

```sql
INSERT INTO Orders (order_id, customer_id, order_date, order_amount) VALUES
(101, 1, '2025-01-05', 5000),
(102, 1, '2025-01-15', 7000),
(103, 1, '2025-02-10', 6500),
(104, 2, '2025-01-12', 4000),
(105, 2, '2025-03-01', 8000),
(106, 3, '2025-02-20', 5500);
```

---

## Expected Output

| customer_id | order_id | order_date | order_amount | previous_order_amount |
| ----------- | -------- | ---------- | ------------ | --------------------- |
| 1           | 101      | 2025-01-05 | 5000         | NULL                  |
| 1           | 102      | 2025-01-15 | 7000         | 5000                  |
| 1           | 103      | 2025-02-10 | 6500         | 7000                  |
| 2           | 104      | 2025-01-12 | 4000         | NULL                  |
| 2           | 105      | 2025-03-01 | 8000         | 4000                  |
| 3           | 106      | 2025-02-20 | 5500         | NULL                  |

---

## Explanation

### Customer 1

| Order | Amount | Previous Amount |
| ----- | ------ | --------------- |
| 101   | 5000   | NULL            |
| 102   | 7000   | 5000            |
| 103   | 6500   | 7000            |

### Customer 2

| Order | Amount | Previous Amount |
| ----- | ------ | --------------- |
| 104   | 4000   | NULL            |
| 105   | 8000   | 4000            |

### Customer 3

Only one order exists, so the previous amount is `NULL`.

---

## Constraints

* `1 <= Orders rows <= 10^5`
* Each customer may place multiple orders.
* Order dates are unique per customer.
* Output should be ordered by `customer_id` and `order_date`.

---

## Follow-Up Variations

1. Find the next order amount using `LEAD()`.
2. Calculate the difference between current and previous order amounts.
3. Find the percentage increase from the previous order.
4. Find consecutive orders placed within 30 days.
5. Rank orders by amount for each customer.
