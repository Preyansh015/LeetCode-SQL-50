# 570. Managers with at Least 5 Direct Reports

<img src="https://img.shields.io/badge/Difficulty-Medium-orange?style=flat-square" alt="Difficulty Medium"> 

## 📝 Problem Statement
Write a solution to find managers with at least five direct reports.

Return the result table in any order.

---

## 📋 Table Schema: `Employee`
| Column Name | Type | Description |
| :--- | :--- | :--- |
| `id` | int | Primary key representing employee ID |
| `name` | varchar | Employee name |
| `department` | varchar | Department name |
| `managerId` | int | ID of the manager (`null` if no manager) |

* No employee will be the manager of themselves.

---

## 🔍 Examples

**Example 1:**

* **Input:** `Employee` table
  
  | id | name | department | managerId |
  | :---: | :--- | :--- | :---: |
  | 101 | John | A | null |
  | 102 | Dan | A | 101 |
  | 103 | James | A | 101 |
  | 104 | Amy | A | 101 |
  | 105 | Anne | A | 101 |
  | 106 | Ron | B | 101 |

* **Output:** 
  
  | name |
  | :--- |
  | John |

* **Explanation:** 
  * Employee with ID `101` (John) is the manager of employees `102`, `103`, `104`, `105`, and `106` (total 5 direct reports).

---

## 💡 Approach & Logic (MS SQL Server)
* Perform an **Inner Self-Join** where table `e1` acts as the manager and table `e2` acts as the direct reports (`e1.id = e2.managerId`).
* Group the results by the manager's `id` and `name`.
* Use the **`HAVING`** clause with `COUNT(e2.id) >= 5` to filter for managers who have 5 or more direct reports.

---

## 💻 MS SQL Code
```sql
SELECT e1.name
FROM Employee e1
JOIN Employee e2 
  ON e1.id = e2.managerId
GROUP BY e1.id, e1.name
HAVING COUNT(e2.id) >= 5;
