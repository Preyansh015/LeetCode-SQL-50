# 1581. Customer Who Visited but Did Not Make Any Transactions

<img src="https://img.shields.io/badge/Difficulty-Easy-brightgreen?style=flat-square" alt="Difficulty Easy"> 

## 📝 Problem Statement
Write a solution to find the IDs of the users who visited without making any transactions and the number of times they made these types of visits.

Return the result table in any order.

---

## 📋 Table Schema

**`Visits` Table:**
| Column Name | Type | Description |
| :--- | :--- | :--- |
| `visit_id` | int | Primary key representing the visit ID |
| `customer_id` | int | ID of the customer who visited |

**`Transactions` Table:**
| Column Name | Type | Description |
| :--- | :--- | :--- |
| `transaction_id` | int | Primary key representing the transaction ID |
| `visit_id` | int | ID of the visit associated with the transaction |
| `amount` | int | Amount of the transaction |

---

## 🔍 Examples

**Example 1:**

* **Input:** 
  * `Visits` table:
    | visit_id | customer_id |
    | :---: | :---: |
    | 1 | 23 |
    | 2 | 9 |
    | 4 | 30 |
    | 5 | 54 |
    | 6 | 96 |
    | 7 | 54 |
    | 8 | 54 |
  
  * `Transactions` table:
    | transaction_id | visit_id | amount |
    | :---: | :---: | :---: |
    | 2 | 5 | 310 |
    | 3 | 5 | 300 |
    | 9 | 5 | 200 |
    | 12 | 1 | 910 |
    | 13 | 2 | 970 |

* **Output:** 
  | customer_id | count_no_trans |
  | :---: | :---: |
  | 54 | 2 |
  | 30 | 1 |
  | 96 | 1 |

* **Explanation:** 
  * Customer 30 visited once and made no transactions (`count_no_trans = 1`).
  * Customer 96 visited once and made no transactions (`count_no_trans = 1`).
  * Customer 54 visited 3 times; visits 7 and 8 had no transactions (`count_no_trans = 2`).

---

## 💡 Approach & Logic (MS SQL Server)
* Use a **`LEFT JOIN`** from `Visits` to `Transactions` on `visit_id` to capture all visits, including those without matching entries in the `Transactions` table.
* Filter for rows where the `transaction_id` is **`NULL`**, which isolates the visits where no transactions occurred.
* Group by `customer_id` and use `COUNT(v.visit_id)` to count how many such visits each customer made.

---

## 💻 MS SQL Code
```sql
SELECT v.customer_id, COUNT(v.visit_id) AS count_no_trans
FROM Visits v
LEFT JOIN Transactions t
  ON v.visit_id = t.visit_id
WHERE t.transaction_id IS NULL
GROUP BY v.customer_id;
