# Monthly Sales Report — Oracle SQL Developer Style Problem

## Problem Statement

Write an Oracle SQL query to calculate the total sales amount for each month from the `SALES` table.

Return:

* Month (`YYYY-MM`)
* Total sales amount for that month

Sort the result by month in ascending order.

---

## Table Schema

```sql
CREATE TABLE SALES (
    SALE_ID NUMBER PRIMARY KEY,
    PRODUCT_NAME VARCHAR2(100),
    SALE_DATE DATE,
    AMOUNT NUMBER(10,2)
);
```

---

## Sample Data

```sql
INSERT INTO SALES VALUES (1, 'Laptop', TO_DATE('2025-01-05', 'YYYY-MM-DD'), 55000);
INSERT INTO SALES VALUES (2, 'Mouse', TO_DATE('2025-01-10', 'YYYY-MM-DD'), 1200);
INSERT INTO SALES VALUES (3, 'Keyboard', TO_DATE('2025-02-02', 'YYYY-MM-DD'), 2500);
INSERT INTO SALES VALUES (4, 'Monitor', TO_DATE('2025-02-15', 'YYYY-MM-DD'), 15000);
INSERT INTO SALES VALUES (5, 'Laptop', TO_DATE('2025-03-01', 'YYYY-MM-DD'), 60000);
INSERT INTO SALES VALUES (6, 'Mouse', TO_DATE('2025-03-12', 'YYYY-MM-DD'), 1500);
INSERT INTO SALES VALUES (7, 'Tablet', TO_DATE('2025-03-18', 'YYYY-MM-DD'), 22000);

COMMIT;
```

---

## Expected Output

| MONTH   | TOTAL_SALES |
| ------- | ----------- |
| 2025-01 | 56200       |
| 2025-02 | 17500       |
| 2025-03 | 83500       |

---

## Explanation

### January 2025

* Laptop → 55000
* Mouse → 1200

Total = `56200`

### February 2025

* Keyboard → 2500
* Monitor → 15000

Total = `17500`

### March 2025

* Laptop → 60000
* Mouse → 1500
* Tablet → 22000

Total = `83500`

---

## Constraints

* `1 <= SALES rows <= 10^5`
* Amount is always positive
* Dates are valid Oracle DATE values
* Output should be sorted month-wise

---

## Follow-Up Variations

1. Find highest sales month
2. Find average monthly sales
3. Find monthly sales per product
4. Compare month-over-month sales growth
5. Find months where total sales exceeded 1 lakh
