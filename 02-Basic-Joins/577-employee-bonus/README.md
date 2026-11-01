# 577. Employee Bonus

<img src="https://img.shields.io/badge/Difficulty-Easy-brightgreen?style=flat-square" alt="Difficulty Easy"> 

## 📝 Problem Statement
Write a solution to report the name and bonus amount of each employee who satisfies either of the following:
* The employee has a bonus less than 1000.
* The employee did not get any bonus.

Return the result table in any order.

---

## 📋 Table Schema

**`Employee` Table:**
| Column Name | Type | Description |
| :--- | :--- | :--- |
| `empId` | int | Primary key representing employee ID |
| `name` | varchar | Employee name |
| `supervisor` | int | ID of the manager |
| `salary` | int | Employee salary |

**`Bonus` Table:**
| Column Name | Type | Description |
| :--- | :--- | :--- |
| `empId` | int | Primary key / Foreign key referencing Employee `empId` |
| `bonus` | int | Bonus amount for the employee |

---

## 🔍 Examples

**Example 1:**

* **Input:** 
  * `Employee` table:
    | empId | name | supervisor | salary |
    | :---: | :--- | :---: | :---: |
    | 3 | Brad | null | 4000 |
    | 1 | John | 3 | 1000 |
    | 2 | Dan | 3 | 2000 |
    | 4 | Thomas | 3 | 4000 |
  
  * `Bonus` table:
    | empId | bonus |
    | :---: | :---: |
    | 2 | 500 |
    | 4 | 2000 |

* **Output:** 
  | name | bonus |
  | :--- | :---: |
  | Brad | null |
  | John | null |
  | Dan | 500 |

* **Explanation:** 
  * Brad and John have no record in the `Bonus` table, so their bonus is `null`.
  * Dan has a bonus of 500, which is less than 1000.
  * Thomas has a bonus of 2000 (not included because it is >= 1000).

---

## 💡 Approach & Logic (MS SQL Server)
* Use a **`LEFT JOIN`** from `Employee` to `Bonus` on `empId` to ensure all employees are included, even those without a matching bonus entry (`NULL`).
* Apply a `WHERE` filter to capture employees whose bonus is strictly less than 1000 (`b.bonus < 1000`) **or** who did not receive any bonus (`b.bonus IS NULL`).

---

## 💻 MS SQL Code
```sql
SELECT e.name, b.bonus
FROM Employee e
LEFT JOIN Bonus b
  ON e.empId = b.empId
WHERE b.bonus < 1000 
   OR b.bonus IS NULL;
