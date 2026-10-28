---

### 584. Find Customer Referee
<img src="https://img.shields.io/badge/Difficulty-Easy-brightgreen?style=flat-square" alt="Difficulty Easy"> 

#### 📝 Problem Statement
Find the names of the customer that are either:
1. Referred by any customer with `id != 2`.
2. Not referred by any customer (`NULL`).

Return the result table in any order.

---

#### 📋 Table Schema: `Customer`
| Column Name | Type | Description |
| :--- | :--- | :--- |
| `id` | int | Primary key (unique values) |
| `name` | varchar | Customer name |
| `referee_id` | int | ID of the customer who referred them |

---

#### 🔍 Examples

**Example 1:**

* **Input:** `Customer` table
  
  | id | name | referee_id |
  | :---: | :---: | :---: |
  | 1 | Will | null |
  | 2 | Jane | null |
  | 3 | Alex | 2 |
  | 4 | Bill | null |
  | 5 | Zack | 1 |
  | 6 | Mark | 2 |

* **Output:** 
  
  | name |
  | :---: |
  | Will |
  | Jane |
  | Bill |
  | Zack |

* **Explanation:** 
  * Customers Will, Jane, and Bill have a `referee_id` of null (not referred by anyone).
  * Customer Zack has a `referee_id` of 1, which is not equal to 2.
  * Customer Alex and Mark are excluded because their `referee_id` is 2.

---

#### 💡 Approach & Logic (MS SQL Server)
* In SQL, comparisons with `NULL` (like `referee_id != 2`) evaluate to `UNKNOWN`, meaning rows with `NULL` values get filtered out automatically.
* To include customers who were not referred by anyone, we must explicitly add `OR referee_id IS NULL` to handle `NULL` values correctly.

---

#### 💻 MS SQL Code
```sql
SELECT name
FROM Customer
WHERE referee_id != 2
   OR referee_id IS NULL;
