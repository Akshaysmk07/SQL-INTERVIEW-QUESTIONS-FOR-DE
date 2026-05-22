# Remove Duplicate Rows — LeetCode Style SQL Problem

## Problem Statement

Write a SQL query to remove duplicate rows from the `Users` table.

A duplicate row is defined as having the same email address.
Keep only the row with the smallest `id` for each duplicate email.

---

## Table Schema

```sql
CREATE TABLE Users (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(255)
);
```

---

## Sample Data

```sql
INSERT INTO Users (id, name, email) VALUES
(1, 'Akshay', 'akshay@gmail.com'),
(2, 'Rahul', 'rahul@gmail.com'),
(3, 'Sneha', 'sneha@gmail.com'),
(4, 'Kiran', 'rahul@gmail.com'),
(5, 'Meera', 'meera@gmail.com'),
(6, 'John', 'akshay@gmail.com'),
(7, 'David', 'john@gmail.com');
```

---

## Expected Table After Deletion

| id | name   | email                                    |
| -- | ------ | ---------------------------------------- |
| 1  | Akshay | [akshay@gmail.com](mailto:akshay@gmail.com) |
| 2  | Rahul  | [rahul@gmail.com](mailto:rahul@gmail.com)   |
| 3  | Sneha  | [sneha@gmail.com](mailto:sneha@gmail.com)   |
| 5  | Meera  | [meera@gmail.com](mailto:meera@gmail.com)   |
| 7  | David  | [john@gmail.com](mailto:john@gmail.com)     |

---

## Explanation

Duplicate emails:

* `akshay@gmail.com` → keep id `1`, remove id `6`
* `rahul@gmail.com` → keep id `2`, remove id `4`

Only the smallest `id` should remain for each email.

---

## Constraints

* `1 <= Users rows <= 10^5`
* Email values may contain duplicates
* `id` values are unique
* Output table should not contain duplicate emails

---

## Follow-Up Variations

1. Remove duplicates based on multiple columns
2. Keep latest row instead of smallest `id`
3. Find duplicate phone numbers
4. Remove duplicates using window functions
5. Count how many duplicate rows were removed
