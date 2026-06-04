# Find Top 2 Products in Each Category — MySQL LeetCode Style Problem

## Problem Statement

Write a MySQL query to find the  **top 2 products with the highest sales amount in each category** .

Return:

* Category
* Product Name
* Sales Amount

If multiple products have the same sales amount, rank them accordingly.

---

## Table Schema

```sql
CREATE TABLE Products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100),
    category VARCHAR(100),
    sales_amount INT
);
```

---

## Sample Data

```sql
INSERT INTO Products (product_id, product_name, category, sales_amount) VALUES
(1, 'iPhone 15', 'Mobile', 120000),
(2, 'Samsung S24', 'Mobile', 110000),
(3, 'OnePlus 12', 'Mobile', 90000),
(4, 'MacBook Air', 'Laptop', 150000),
(5, 'Dell XPS', 'Laptop', 140000),
(6, 'HP Pavilion', 'Laptop', 120000),
(7, 'Boat Airdopes', 'Accessories', 5000),
(8, 'Sony Headphones', 'Accessories', 15000),
(9, 'JBL Speaker', 'Accessories', 12000);
```

---

## Expected Output

| category    | product_name    | sales_amount |
| ----------- | --------------- | -----------: |
| Accessories | Sony Headphones |        15000 |
| Accessories | JBL Speaker     |        12000 |
| Laptop      | MacBook Air     |       150000 |
| Laptop      | Dell XPS        |       140000 |
| Mobile      | iPhone 15       |       120000 |
| Mobile      | Samsung S24     |       110000 |

---

## Explanation

### Mobile

| Product     |  Sales |
| ----------- | -----: |
| iPhone 15   | 120000 |
| Samsung S24 | 110000 |
| OnePlus 12  |  90000 |

Top 2 products:

* iPhone 15
* Samsung S24

### Laptop

| Product     |  Sales |
| ----------- | -----: |
| MacBook Air | 150000 |
| Dell XPS    | 140000 |
| HP Pavilion | 120000 |

Top 2 products:

* MacBook Air
* Dell XPS

### Accessories

| Product         | Sales |
| --------------- | ----: |
| Sony Headphones | 15000 |
| JBL Speaker     | 12000 |
| Boat Airdopes   |  5000 |

Top 2 products:

* Sony Headphones
* JBL Speaker

---

## Constraints

* `1 <= Products rows <= 10^5`
* Sales amount is always positive.
* Category values are non-null.
* Each category may contain multiple products.

---

## Follow-Up Variations

1. Find top 3 products in each category.
2. Find the highest-selling product in each category.
3. Find the bottom 2 products in each category.
4. Rank products within each category by sales.
5. Find categories where the top product's sales exceed 1,00,000.
