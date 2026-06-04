# Find Consecutive Login Days — MySQL LeetCode Style Problem

## Problem Statement

Write a MySQL query to find users who logged in on  **two or more consecutive days** .

Return:

* User ID
* Login Date
* Previous Login Date

A login is considered consecutive if the difference between the current login date and the previous login date is exactly  **1 day** .

Sort the output by `user_id` and `login_date`.

---

## Table Schema

```sql
CREATE TABLE Logins (
    login_id INT PRIMARY KEY,
    user_id INT,
    login_date DATE
);
```

---

## Sample Data

```sql
INSERT INTO Logins (login_id, user_id, login_date) VALUES
(1, 101, '2025-01-01'),
(2, 101, '2025-01-02'),
(3, 101, '2025-01-04'),
(4, 102, '2025-01-05'),
(5, 102, '2025-01-06'),
(6, 102, '2025-01-07'),
(7, 103, '2025-01-03'),
(8, 103, '2025-01-05');
```

---

## Expected Output

| user_id | login_date | previous_login_date |
| ------- | ---------- | ------------------- |
| 101     | 2025-01-02 | 2025-01-01          |
| 102     | 2025-01-06 | 2025-01-05          |
| 102     | 2025-01-07 | 2025-01-06          |

---

## Explanation

### User 101

| Login Date | Previous Login | Consecutive |
| ---------- | -------------- | ----------- |
| 2025-01-01 | NULL           | No          |
| 2025-01-02 | 2025-01-01     | Yes         |
| 2025-01-04 | 2025-01-02     | No          |

### User 102

| Login Date | Previous Login | Consecutive |
| ---------- | -------------- | ----------- |
| 2025-01-05 | NULL           | No          |
| 2025-01-06 | 2025-01-05     | Yes         |
| 2025-01-07 | 2025-01-06     | Yes         |

### User 103

| Login Date | Previous Login | Consecutive |
| ---------- | -------------- | ----------- |
| 2025-01-03 | NULL           | No          |
| 2025-01-05 | 2025-01-03     | No          |

---

## Constraints

* `1 <= Logins rows <= 10^5`
* A user can have multiple login records.
* Each user has at most one login per day.
* Output should be sorted by `user_id` and `login_date`.

---

## Follow-Up Variations

1. Find users with  **3 or more consecutive login days** .
2. Find the longest consecutive login streak for each user.
3. Find users who logged in every day of a given month.
4. Calculate the gap (in days) between consecutive logins.
5. Find users whose latest two logins were consecutive.
