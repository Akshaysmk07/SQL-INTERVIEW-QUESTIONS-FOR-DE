# Employees Joined in Last 30 Days — Oracle SQL Developer Style Problem

## Problem Statement

Write an Oracle SQL query to find all employees who joined in the last 30 days from the current system date.

Return:

* Employee ID
* Employee Name
* Department
* Joining Date

Sort the result by joining date in descending order.

---

## Table Schema

```sql
CREATE TABLE EMPLOYEES (
    EMPLOYEE_ID NUMBER PRIMARY KEY,
    EMPLOYEE_NAME VARCHAR2(100),
    DEPARTMENT VARCHAR2(100),
    JOIN_DATE DATE,
    SALARY NUMBER(10,2)
);
```

---

## Sample Data

```sql
INSERT INTO EMPLOYEES VALUES (1, 'Akshay', 'Engineering', SYSDATE - 5, 70000);
INSERT INTO EMPLOYEES VALUES (2, 'Rahul', 'Finance', SYSDATE - 15, 65000);
INSERT INTO EMPLOYEES VALUES (3, 'Sneha', 'HR', SYSDATE - 40, 50000);
INSERT INTO EMPLOYEES VALUES (4, 'Kiran', 'Engineering', SYSDATE - 25, 80000);
INSERT INTO EMPLOYEES VALUES (5, 'Meera', 'HR', SYSDATE - 60, 55000);

COMMIT;
```

---

## Expected Output

| EMPLOYEE_ID | EMPLOYEE_NAME | DEPARTMENT  | JOIN_DATE   |
| ----------- | ------------- | ----------- | ----------- |
| 1           | Akshay        | Engineering | Recent Date |
| 2           | Rahul         | Finance     | Recent Date |
| 4           | Kiran         | Engineering | Recent Date |

---

## Explanation

Employees who joined within the last 30 days:

* Akshay → joined 5 days ago
* Rahul → joined 15 days ago
* Kiran → joined 25 days ago

Employees joined more than 30 days ago should not be included.

---

## Constraints

* `1 <= EMPLOYEES rows <= 10^5`
* JOIN_DATE is a valid Oracle DATE
* Use Oracle date functions
* Output should be sorted by latest joining date first

---

## Follow-Up Variations

1. Find employees joined in the current month
2. Find employees joined in the last 7 days
3. Count employees joined department-wise
4. Find employees who completed 1 year
5. Find employees joined between two dates
