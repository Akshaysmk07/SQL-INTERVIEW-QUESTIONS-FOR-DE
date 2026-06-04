# Find Latest Login Per User — MySQL LeetCode Style Problem

## Problem Statement

Write a MySQL query to find the **most recent login date** for each user.

Return:

* User ID
* Latest Login Date

Sort the output by `user_id`.

---

## Table Schema

```sql
CREATE TABLE Logins (
    login_id INT PRIMARY KEY,
    user_id INT,
    login_datetime DATETIME
);
```

---

## Sample Data

```sql
INSERT INTO Logins (login_id, user_id, login_datetime) VALUES
(1, 101, '2025-01-05 09:15:00'),
(2, 102, '2025-01-06 10:30:00'),
(3, 101, '2025-01-10 08:45:00'),
(4, 103, '2025-01-08 14:20:00'),
(5, 102, '2025-01-15 16:10:00'),
(6, 101, '2025-01-12 11:00:00'),
(7, 103, '2025-01-20 18:30:00');
```

---

## Expected Output

| user_id | latest_login        |
| ------- | ------------------- |
| 101     | 2025-01-12 11:00:00 |
| 102     | 2025-01-15 16:10:00 |
| 103     | 2025-01-20 18:30:00 |

---

## Explanation

### User 101

Login history:

* 2025-01-05 09:15:00
* 2025-01-10 08:45:00
* 2025-01-12 11:00:00

Latest login = **2025-01-12 11:00:00**

### User 102

Login history:

* 2025-01-06 10:30:00
* 2025-01-15 16:10:00

Latest login = **2025-01-15 16:10:00**

### User 103

Login history:

* 2025-01-08 14:20:00
* 2025-01-20 18:30:00

Latest login = **2025-01-20 18:30:00**

---

## Constraints

* `1 <= Logins rows <= 10^5`
* A user can have multiple login records.
* `login_datetime` values are valid.
* Output should be sorted by `user_id`.

---

## Follow-Up Variations

1. Find the first login per user.
2. Find users who logged in more than once.
3. Find the time difference between the latest and previous login.
4. Find users who have not logged in during the last 30 days.
5. Find the latest login along with the total number of logins per user.
