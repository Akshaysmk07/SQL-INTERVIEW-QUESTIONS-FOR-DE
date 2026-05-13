
# Customers Who Never Placed Orders — LeetCode Style SQL Problem

## Problem Statement

Write a SQL query to find all customers who never placed any orders.

Return the customer names from the `Customers` table who do not have a matching record in the `Orders` table.

---

## Table Schema

### Customers Table

```sql
CREATE TABLE Customers (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(100)
);
```

### Orders Table

```sql
CREATE TABLE Orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE
);
```

---

## Sample Data

### Customers

```sql
INSERT INTO Customers (customer_id, customer_name) VALUES
(1, 'Akshay'),
(2, 'Rahul'),
(3, 'Sneha'),
(4, 'Kiran'),
(5, 'Meera');
```

### Orders

```sql
INSERT INTO Orders (order_id, customer_id, order_date) VALUES
(101, 1, '2025-01-10'),
(102, 3, '2025-01-15'),
(103, 1, '2025-02-01'),
(104, 5, '2025-02-12');
```

---

## Expected Output

| customer_name |
| ------------- |
| Rahul         |
| Kiran         |

---

## Explanation

* Akshay placed orders
* Sneha placed orders
* Meera placed orders
* Rahul and Kiran never placed any orders

---

## Constraints

* `1 <= Customers rows <= 10^5`
* `1 <= Orders rows <= 10^5`
* A customer can place multiple orders
* Output order does not matter

---

## Follow-Up Variations

1. Find customers with more than 5 orders
2. Find customers who ordered in the last 30 days
3. Find customers with the highest number of orders
4. Find customers who ordered every month
5. Find products never ordered
