# Find Duplicate Emails — LeetCode Style SQL Problem

## Problem Statement

Write a SQL query to find all duplicate emails from the `Users` table.

Return only the email addresses that appear more than once.

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

## Expected Output

| email                                    |
| ---------------------------------------- |
| [akshay@gmail.com](mailto:akshay@gmail.com) |
| [rahul@gmail.com](mailto:rahul@gmail.com)   |

---

## Explanation

* `akshay@gmail.com` appears 2 times
* `rahul@gmail.com` appears 2 times
* Other emails appear only once

---

## Constraints

* `1 <= Users rows <= 10^5`
* Email values can contain duplicates
* Email format is valid
* Output order does not matter

---

## Follow-Up Variations

1. Find duplicate records based on multiple columns
2. Delete duplicate rows while keeping one record
3. Find users with duplicate phone numbers
4. Find duplicate emails created on the same day
5. Count occurrences of each duplicate email
