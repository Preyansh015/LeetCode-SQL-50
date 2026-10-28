# 📊 LeetCode Top SQL 50 - Solutions

<p align="center">
  <img src="https://img.shields.io/badge/Platform-LeetCode-orange?style=for-the-badge&logo=leetcode&logoColor=white" alt="LeetCode">
  <img src="https://img.shields.io/badge/Language-SQL%20%2F%20T--SQL-blue?style=for-the-badge&logo=postgresql&logoColor=white" alt="SQL">
  <img src="https://img.shields.io/badge/Status-In%20Progress-brightgreen?style=for-the-badge" alt="Status">
</p>

---

## 📂 01. Select

### 1757. Recyclable and Low Fat Products
<img src="https://img.shields.io/badge/Difficulty-Easy-brightgreen?style=flat-square" alt="Difficulty Easy"> 

#### 📝 Problem Statement
Write a solution to find the IDs of products that are both low fat and recyclable.

Return the result table in any order.

---

#### 📋 Table Schema: `Products`
| Column Name | Type | Description |
| :--- | :--- | :--- |
| `product_id` | int | Primary key (unique values) |
| `low_fats` | enum | Category ('Y' means low fat, 'N' means not low fat) |
| `recyclable` | enum | Category ('Y' means recyclable, 'N' means not recyclable) |

---

#### 🔍 Examples

**Example 1:**

* **Input:** `Products` table
  
  | product_id | low_fats | recyclable |
  | :---: | :---: | :---: |
  | 0 | Y | N |
  | 1 | Y | Y |
  | 2 | N | Y |
  | 3 | Y | Y |
  | 4 | N | N |

* **Output:** 
  
  | product_id |
  | :---: |
  | 1 |
  | 3 |

* **Explanation:** Only products 1 and 3 are both low fat and recyclable.

---

#### 💡 Approach & Logic
* We need to select the `product_id` from the `Products` table.
* We apply a `WHERE` condition to filter rows where **both** `low_fats` equals `'Y'` and `recyclable` equals `'Y'` using the logical `AND` operator.

---

#### 💻 SQL Code
```sql
SELECT product_id
FROM Products
WHERE low_fats = 'Y' 
  AND recyclable = 'Y';
