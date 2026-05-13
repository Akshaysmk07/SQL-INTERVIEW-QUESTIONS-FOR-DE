# Customers Who Never Placed Orders — SQL Solution

## Approach 1: Using `LEFT JOIN`

### Query

```sql
SELECT c.customer_name
FROM Customers c
LEFT JOIN Orders o
ON c.customer_id = o.customer_id
WHERE o.order_id IS NULL;
```

---

# Explanation

## Step 1 — Perform LEFT JOIN

```sql
LEFT JOIN Orders o
ON c.customer_id = o.customer_id
```

Returns:

- All customers
- Matching orders if available

If no matching order exists,
order columns become `NULL`.

---

## Step 2 — Filter Customers Without Orders

```sql
WHERE o.order_id IS NULL
```

Keeps only customers who never placed orders.

---

# Example

## Customers Table

| customer_id | customer_name |
| ----------- | ------------- |
| 1           | Akshay        |
| 2           | Rahul         |
| 3           | Sneha         |
| 4           | Kiran         |

---

## Orders Table

| order_id | customer_id |
| -------- | ----------- |
| 101      | 1           |
| 102      | 3           |

---

# LEFT JOIN Result

| customer_name | order_id |
| ------------- | -------- |
| Akshay        | 101      |
| Rahul         | NULL     |
| Sneha         | 102      |
| Kiran         | NULL     |

---

# Final Output

| customer_name |
| ------------- |
| Rahul         |
| Kiran         |

---

# Why `LEFT JOIN`?

`LEFT JOIN` keeps all rows from the left table (`Customers`)
even when no match exists in `Orders`.

This makes it perfect for:

- Missing records
- Unmatched rows
- Anti-join problems

---

# Alternative Approach Using `NOT IN`

```sql
SELECT customer_name
FROM Customers
WHERE customer_id NOT IN (
    SELECT customer_id
    FROM Orders
);
```

---

# Alternative Approach Using `NOT EXISTS`

```sql
SELECT c.customer_name
FROM Customers c
WHERE NOT EXISTS (
    SELECT 1
    FROM Orders o
    WHERE c.customer_id = o.customer_id
);
```

---

# Best Interview Approach

## Recommended

```sql
LEFT JOIN + IS NULL
```

because:

- Easy to understand
- Readable
- Common SQL interview pattern

---

# Important Interview Concept

## Difference Between JOIN Types

### INNER JOIN

Returns only matching rows.

### LEFT JOIN

Returns:

- All rows from left table
- Matching rows from right table
- `NULL` for unmatched rows

---

# Common Real-World Use Cases

- Customers without orders
- Employees without managers
- Products never sold
- Students without enrollments
- Users without logins
