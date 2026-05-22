# Average Salary Department Wise — Oracle SQL Developer Style Problem

## Problem Statement

Write an Oracle SQL query to calculate the average salary for each department from the `EMPLOYEES` table.

Return:

* Department name
* Average salary

Sort the result by average salary in descending order.

---

## Table Schema

```sql
CREATE TABLE EMPLOYEES (
    EMPLOYEE_ID NUMBER PRIMARY KEY,
    EMPLOYEE_NAME VARCHAR2(100),
    DEPARTMENT VARCHAR2(100),
    SALARY NUMBER(10,2)
);
```

---

## Sample Data

```sql
INSERT INTO EMPLOYEES VALUES (1, 'Akshay', 'Engineering', 90000);
INSERT INTO EMPLOYEES VALUES (2, 'Rahul', 'Engineering', 80000);
INSERT INTO EMPLOYEES VALUES (3, 'Sneha', 'HR', 50000);
INSERT INTO EMPLOYEES VALUES (4, 'Kiran', 'Finance', 75000);
INSERT INTO EMPLOYEES VALUES (5, 'Meera', 'HR', 60000);
INSERT INTO EMPLOYEES VALUES (6, 'John', 'Finance', 85000);

COMMIT;
```

---

## Expected Output

| DEPARTMENT  | AVG_SALARY |
| ----------- | ---------- |
| Engineering | 85000      |
| Finance     | 80000      |
| HR          | 55000      |

---

## Explanation

### Engineering

* 90000
* 80000

Average = `85000`

### Finance

* 75000
* 85000

Average = `80000`

### HR

* 50000
* 60000

Average = `55000`

---

## Constraints

* `1 <= EMPLOYEES rows <= 10^5`
* Salary is always positive
* Department values are non-null
* Output should be sorted by highest average salary first

---

## Follow-Up Variations

1. Find departments with average salary above 70000
2. Find highest salary per department
3. Find lowest salary per department
4. Find employee count per department
5. Find departments where average salary is below company average
