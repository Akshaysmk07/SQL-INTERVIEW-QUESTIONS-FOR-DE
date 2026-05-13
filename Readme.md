# SQL Preparation Roadmap for Product-Based Companies

This list is structured exactly like real interviews:

* Easy → screening rounds
* Medium → core interview rounds
* Advanced → product-company elimination level

Focus especially on:

* Window functions
* CTEs
* Business logic
* Optimization thinking

---

# 10 EASY SQL QUESTIONS

These build your fundamentals.

---

## 1. Second Highest Salary

```sql
Find the second highest salary from Employee table.
```

---

## 2. Find Duplicate Records

```sql
Find duplicate emails in Users table.
```

---

## 3. Top 3 Salaries

```sql
Get top 3 salaries from Employee table.
```

---

## 4. Count Employees by Department

```sql
Find employee count in each department.
```

---

## 5. Customers Without Orders

```sql
Find customers who never placed orders.
```

---

## 6. Highest Salary in Each Department

```sql
Find highest paid employee per department.
```

---

## 7. Remove Duplicate Rows

```sql
Delete duplicate records keeping latest one.
```

---

## 8. Monthly Sales

```sql
Calculate monthly sales totals.
```

---

## 9. Employees Joined in Last 30 Days

```sql
Find recently joined employees.
```

---

## 10. Average Salary

```sql
Find average salary department-wise.
```

---

# 40 MEDIUM SQL QUESTIONS

These are VERY important for:

* Google
* Amazon
* Walmart
* Uber
* Swiggy
* Atlassian

---

# Window Function Questions

## 1.

```sql
Rank employees by salary department-wise.
```

## 2.

```sql
Find top 2 products in each category.
```

## 3.

```sql
Find previous order amount using LAG().
```

## 4.

```sql
Find salary difference from previous employee.
```

## 5.

```sql
Calculate running total of sales.
```

## 6.

```sql
Find moving average of 7 days.
```

## 7.

```sql
Find first order date for every customer.
```

## 8.

```sql
Find latest login per user.
```

## 9.

```sql
Find consecutive login days.
```

## 10.

```sql
Find users active 3 consecutive days.
```

---

# JOIN-Based Questions

## 11.

```sql
Find employees earning more than managers.
```

## 12.

```sql
Find manager with highest team size.
```

## 13.

```sql
Find customers who ordered all products.
```

## 14.

```sql
Find mutual friends.
```

## 15.

```sql
Find products never sold.
```

## 16.

```sql
Find missing transactions.
```

## 17.

```sql
Find duplicate transactions.
```

## 18.

```sql
Find orders with delayed shipping.
```

## 19.

```sql
Find departments without employees.
```

## 20.

```sql
Find customers with maximum spend.
```

---

# Aggregation Questions

## 21.

```sql
Find daily active users.
```

## 22.

```sql
Find retention rate month-wise.
```

## 23.

```sql
Calculate average order value.
```

## 24.

```sql
Find repeat customers.
```

## 25.

```sql
Find revenue growth percentage.
```

## 26.

```sql
Find top selling category monthly.
```

## 27.

```sql
Find customer churn.
```

## 28.

```sql
Find conversion rates.
```

## 29.

```sql
Find bounce rate.
```

## 30.

```sql
Find cart abandonment percentage.
```

---

# CTE + Subquery Questions

## 31.

```sql
Find nth highest salary.
```

## 32.

```sql
Find median salary.
```

## 33.

```sql
Split comma-separated values.
```

## 34.

```sql
Recursive employee hierarchy.
```

## 35.

```sql
Generate calendar table.
```

## 36.

```sql
Find gaps in sequence.
```

## 37.

```sql
Find overlapping date ranges.
```

## 38.

```sql
Find continuous streaks.
```

## 39.

```sql
Pivot rows into columns.
```

## 40.

```sql
Unpivot columns into rows.
```

---

# 50 ADVANCED SQL QUESTIONS

These are PRODUCT-COMPANY LEVEL.

If you can solve most of these:

* Google
* Meta
* Uber
* Airbnb
* Snowflake
* Databricks
  becomes realistic.

---

# Advanced Window Function Problems

## 1.

```sql
Sessionization of user activity.
```

## 2.

```sql
Calculate rolling retention.
```

## 3.

```sql
Find DAU/WAU/MAU.
```

## 4.

```sql
Detect fraudulent transactions.
```

## 5.

```sql
Find peak concurrent users.
```

## 6.

```sql
Calculate percentile rankings.
```

## 7.

```sql
Find time spent between events.
```

## 8.

```sql
Customer lifetime value calculation.
```

## 9.

```sql
Revenue cohort analysis.
```

## 10.

```sql
Calculate stickiness ratio.
```

---

# Real Business Problems

## 11.

```sql
Design funnel analysis query.
```

## 12.

```sql
A/B test result analysis.
```

## 13.

```sql
Subscription renewal prediction metrics.
```

## 14.

```sql
Fraud detection rules.
```

## 15.

```sql
Recommendation engine candidate generation.
```

## 16.

```sql
Inventory stockout prediction metrics.
```

## 17.

```sql
Marketplace supply-demand imbalance.
```

## 18.

```sql
Delivery ETA accuracy analysis.
```

## 19.

```sql
Search click-through rate analytics.
```

## 20.

```sql
Ad conversion attribution.
```

---

# Complex CTE Problems

## 21.

```sql
Recursive graph traversal.
```

## 22.

```sql
Detect cyclic hierarchy.
```

## 23.

```sql
Shortest path calculation.
```

## 24.

```sql
Organizational tree traversal.
```

## 25.

```sql
Complex dependency resolution.
```

---

# Optimization Questions

## 26.

```sql
Optimize slow JOIN query.
```

## 27.

```sql
Index optimization scenario.
```

## 28.

```sql
Partition pruning use case.
```

## 29.

```sql
Query execution plan analysis.
```

## 30.

```sql
Reduce shuffle in distributed SQL systems.
```

---

# Advanced Analytics Questions

## 31.

```sql
Multi-touch attribution modeling.
```

## 32.

```sql
Customer segmentation using RFM.
```

## 33.

```sql
Dynamic pricing analysis.
```

## 34.

```sql
Revenue leakage detection.
```

## 35.

```sql
Anomaly detection in metrics.
```

## 36.

```sql
Detect bot traffic patterns.
```

## 37.

```sql
Forecast trend analysis preparation.
```

## 38.

```sql
Event stream deduplication.
```

## 39.

```sql
Real-time leaderboard query.
```

## 40.

```sql
Warehouse utilization analytics.
```

---

# Data Engineering-Focused SQL

## 41.

```sql
CDC (Change Data Capture) merge logic.
```

## 42.

```sql
SCD Type 2 implementation.
```

## 43.

```sql
Incremental load logic.
```

## 44.

```sql
Late arriving dimensions handling.
```

## 45.

```sql
Deduplication at scale.
```

## 46.

```sql
Event-time vs processing-time analysis.
```

## 47.

```sql
Data quality validation framework queries.
```

## 48.

```sql
Streaming aggregation logic.
```

## 49.

```sql
Partition skew analysis.
```

## 50.

```sql
Build star schema aggregation query.
```

---

# Most Important Topics (Must Master)

## Window Functions

You absolutely need mastery in:

```sql
ROW_NUMBER()
RANK()
DENSE_RANK()
LAG()
LEAD()
NTILE()
FIRST_VALUE()
LAST_VALUE()
SUM() OVER()
AVG() OVER()
```

---

# Important SQL Concepts

## CTEs

```sql
WITH cte AS ()
```

## Recursive CTEs

```sql
WITH RECURSIVE
```

## CASE WHEN

```sql
CASE WHEN THEN END
```

## EXISTS vs IN

## UNION vs UNION ALL

## INNER vs LEFT JOIN

## Partitioning Concepts

## Query Optimization

---

# Recommended Preparation Order

## Phase 1

* Easy questions
* JOINs
* GROUP BY
* Basic aggregation

## Phase 2

* Window functions
* CTEs
* Ranking
* Rolling metrics

## Phase 3

* Business problems
* Cohort analysis
* Funnel analysis
* Optimization

## Phase 4

* Timed mock interviews
* Real interview datasets
* Complex analytics

---

# Interview Reality

For top product companies:

### 70% of rejection happens because of:

* Weak SQL
* Weak business logic
* Poor optimization understanding

Not because of coding.

If you deeply master:

* Window functions
* CTEs
* Analytics SQL
* Business metrics

You can outperform many candidates with more experience.
