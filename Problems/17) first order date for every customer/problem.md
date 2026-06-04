# Find First Order Date for Every Customer — MySQL LeetCode Style Problem

## Problem Statement

Write a MySQL query to find the **first order date** for every customer.

Return:

* Customer ID
* First Order Date

Sort the output by `customer_id`.

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
(101, 1, '2025-01-10', 5000),
(102, 2, '2025-01-12', 7000),
(103, 1, '2025-02-05', 3000),
(104, 3, '2025-01-15', 6000),
(105, 2, '2025-03-20', 4000),
(106, 1, '2025-01-05', 2000),
(107, 3, '2025-02-10', 5000);
```

---

## Expected Output

| customer_id | first_order_date |
| ----------- | ---------------- |
| 1           | 2025-01-05       |
| 2           | 2025-01-12       |
| 3           | 2025-01-15       |

---

## Explanation

### Customer 1

Orders:

* 2025-01-10
* 2025-02-05
* 2025-01-05

First order date = **2025-01-05**

### Customer 2

Orders:

* 2025-01-12
* 2025-03-20

First order date = **2025-01-12**

### Customer 3

Orders:

* 2025-01-15
* 2025-02-10

First order date = **2025-01-15**

---

## Constraints

* `1 <= Orders rows <= 10^5`
* Each customer can have multiple orders.
* Order dates are valid.
* Output should be sorted by `customer_id`.

---

## Follow-Up Variations

1. Find the last order date for every customer.
2. Find the first order amount for every customer.
3. Find customers whose first order was above ₹5,000.
4. Find the number of days since each customer's first order.
5. Find the first and last order dates for every customer in a single query.
