# 📊 LeetCode Top SQL 50

This repository contains my solutions to the **LeetCode Top SQL 50** study plan. Solutions are optimized and structured to build a strong data science and analytics portfolio.

---

## 📂 01. Select

### 1757. Recyclable and Low Fat Products
**Difficulty:** Easy  
**Link:** [LeetCode Problem 1757](https://leetcode.com/problems/recylable-and-low-fat-products/)

#### 📝 Problem Statement
Write a solution to find the IDs of products that are both low fat and recyclable.

Return the result table in any order.

**Table: `Products`**
| Column Name | Type |
| :--- | :--- |
| product_id | int |
| low_fats | enum |
| recyclable | enum |

* `product_id` is the primary key (column with unique values) for this table.
* `low_fats` is an ENUM of type ('Y', 'N') where 'Y' means low fat and 'N' means not low fat.
* `recyclable` is an ENUM of type ('Y', 'N') where 'Y' means recyclable and 'N' means not recyclable.

#### 💡 Approach
* Use a `SELECT` statement to retrieve the `product_id` column.
* Apply a `WHERE` clause combined with the `AND` operator to filter rows where both `low_fats = 'Y'` and `recyclable = 'Y'`.

#### 💻 SQL Code
```sql
SELECT product_id
FROM Products
WHERE low_fats = 'Y' 
  AND recyclable = 'Y';
