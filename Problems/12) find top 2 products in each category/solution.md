# Find Top 2 Products in Each Category — MySQL Solution

## Approach: Using `RANK()`

### Query

```sql
SELECT
    category,
    product_name,
    sales_amount
FROM (
    SELECT
        category,
        product_name,
        sales_amount,
        RANK() OVER (
            PARTITION BY category
            ORDER BY sales_amount DESC
        ) AS rnk
    FROM Products
) t
WHERE rnk <= 2
ORDER BY category, sales_amount DESC;
```

---

# Explanation

## Step 1 — Partition by Category

```sql
PARTITION BY category
```

Creates separate ranking groups for each category.

Example:

- Mobile
- Laptop
- Accessories

---

## Step 2 — Rank Products by Sales

```sql
ORDER BY sales_amount DESC
```

Highest selling product receives Rank 1.

---

## Step 3 — Assign Ranks

```sql
RANK() OVER (...)
```

Products having the same sales amount receive the same rank.

Example:

| Product     | Sales  | Rank |
| ----------- | ------ | ---- |
| iPhone 15   | 120000 | 1    |
| Samsung S24 | 110000 | 2    |
| OnePlus 12  | 90000  | 3    |

---

## Step 4 — Keep Top 2

```sql
WHERE rnk <= 2
```

Returns only Rank 1 and Rank 2 products from every category.

---

# Output

| category    | product_name    | sales_amount |
| ----------- | --------------- | ------------ |
| Accessories | Sony Headphones | 15000        |
| Accessories | JBL Speaker     | 12000        |
| Laptop      | MacBook Air     | 150000       |
| Laptop      | Dell XPS        | 140000       |
| Mobile      | iPhone 15       | 120000       |
| Mobile      | Samsung S24     | 110000       |

---

# Example Ranking

## Mobile

| Product     | Sales  | Rank |
| ----------- | ------ | ---- |
| iPhone 15   | 120000 | 1    |
| Samsung S24 | 110000 | 2    |
| OnePlus 12  | 90000  | 3    |

---

## Laptop

| Product     | Sales  | Rank |
| ----------- | ------ | ---- |
| MacBook Air | 150000 | 1    |
| Dell XPS    | 140000 | 2    |
| HP Pavilion | 120000 | 3    |

---

## Accessories

| Product         | Sales | Rank |
| --------------- | ----- | ---- |
| Sony Headphones | 15000 | 1    |
| JBL Speaker     | 12000 | 2    |
| Boat Airdopes   | 5000  | 3    |

---

# What If There Are Ties?

Suppose:

| Product     | Sales  |
| ----------- | ------ |
| iPhone 15   | 120000 |
| Samsung S24 | 120000 |
| OnePlus 12  | 90000  |

Using `RANK()`:

| Product     | Rank |
| ----------- | ---- |
| iPhone 15   | 1    |
| Samsung S24 | 1    |
| OnePlus 12  | 3    |

`WHERE rnk <= 2` returns both tied products.

---

# Alternative Using `DENSE_RANK()`

```sql
SELECT
    category,
    product_name,
    sales_amount
FROM (
    SELECT
        category,
        product_name,
        sales_amount,
        DENSE_RANK() OVER (
            PARTITION BY category
            ORDER BY sales_amount DESC
        ) AS rnk
    FROM Products
) t
WHERE rnk <= 2;
```

Difference:

| Function     | Ranking Example |
| ------------ | --------------- |
| RANK()       | 1,1,3           |
| DENSE_RANK() | 1,1,2           |

---

# Follow-Up Variations

## Top 3 Products Per Category

```sql
WHERE rnk <= 3;
```

---

## Highest Selling Product Per Category

```sql
WHERE rnk = 1;
```

---

## Bottom 2 Products Per Category

```sql
SELECT *
FROM (
    SELECT
        category,
        product_name,
        sales_amount,
        RANK() OVER (
            PARTITION BY category
            ORDER BY sales_amount ASC
        ) AS rnk
    FROM Products
) t
WHERE rnk <= 2;
```

---

## Categories Where Top Product Sales Exceed 100000

```sql
SELECT *
FROM (
    SELECT
        category,
        product_name,
        sales_amount,
        RANK() OVER (
            PARTITION BY category
            ORDER BY sales_amount DESC
        ) AS rnk
    FROM Products
) t
WHERE rnk = 1
  AND sales_amount > 100000;
```

---

# Interview Tip

Use:

- `ROW_NUMBER()` → Exactly N rows per category.
- `RANK()` → Include ties, gaps allowed.
- `DENSE_RANK()` → Include ties, no gaps.

For this problem, since the statement says:

> "If multiple products have the same sales amount, rank them accordingly."

`RANK()` is the most appropriate choice.
