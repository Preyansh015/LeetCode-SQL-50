# 197. Rising Temperature

<img src="https://img.shields.io/badge/Difficulty-Easy-brightgreen?style=flat-square" alt="Difficulty Easy"> 

## 📝 Problem Statement
Write a solution to find all dates' `id` with higher temperatures compared to its previous calendar dates (yesterday).

Return the result table in any order.

---

## 📋 Table Schema: `Weather`
| Column Name | Type | Description |
| :--- | :--- | :--- |
| `id` | int | Primary key representing the record ID |
| `recordDate` | date | Date of the weather record |
| `temperature` | int | Temperature recorded on that day |

---

## 🔍 Examples

**Example 1:**

* **Input:** `Weather` table
  
  | id | recordDate | temperature |
  | :---: | :---: | :---: |
  | 1 | 2015-01-01 | 10 |
  | 2 | 2015-01-02 | 25 |
  | 3 | 2015-01-03 | 20 |
  | 4 | 2015-01-04 | 30 |

* **Output:** 
  
  | id |
  | :---: |
  | 2 |
  | 4 |

* **Explanation:** 
  * On `2015-01-02`, the temperature was `25`, which is higher than the previous day (`10`).
  * On `2015-01-04`, the temperature was `30`, which is higher than the previous day (`20`).

---

## 💡 Approach & Logic (MS SQL Server)
* Perform a **Self-Join** on the `Weather` table (aliasing as `w1` for today and `w2` for yesterday).
* Use the built-in MS SQL Server function `DATEDIFF(DAY, w2.recordDate, w1.recordDate) = 1` to ensure `w1` is exactly one day after `w2`.
* Add a condition `w1.temperature > w2.temperature` to filter for days where the temperature increased relative to the previous day.

---

## 💻 MS SQL Code
```sql
SELECT w1.id
FROM Weather w1
JOIN Weather w2
  ON DATEDIFF(DAY, w2.recordDate, w1.recordDate) = 1
 AND w1.temperature > w2.temperature;
