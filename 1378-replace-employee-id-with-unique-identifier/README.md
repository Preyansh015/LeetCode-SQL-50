---

### 1378. Replace Employee ID With The Unique Identifier
<img src="https://img.shields.io/badge/Difficulty-Easy-brightgreen?style=flat-square" alt="Difficulty Easy"> 

#### 📝 Problem Statement
Write a solution to show the unique ID of each user. If a user does not have a unique ID, show `null` instead.

Return the result table in any order.

---

#### 📋 Table Schema
**`Employees` Table:**
| Column Name | Type | Description |
| :--- | :--- | :--- |
| `id` | int | Primary key representing the employee ID |
| `name` | varchar | Employee name |

**`EmployeeUNI` Table:**
| Column Name | Type | Description |
| :--- | :--- | :--- |
| `id` | int | Employee ID |
| `unique_id` | int | Corresponding unique ID (`id`, `unique_id` is the primary key) |

---

#### 🔍 Examples

**Example 1:**

* **Input:** 
  * `Employees` table:
    | id | name |
    | :---: | :--- |
    | 1 | Alice |
    | 7 | Bob |
    | 11 | Meir |
    | 90 | Winston |
    | 3 | Jonathan |
  
  * `EmployeeUNI` table:
    | id | unique_id |
    | :---: | :---: |
    | 3 | 1 |
    | 11 | 2 |
    | 90 | 3 |

* **Output:** 
  | unique_id | name |
  | :---: | :--- |
  | null | Alice |
  | null | Bob |
  | 2 | Meir |
  | 3 | Winston |
  | 1 | Jonathan |

* **Explanation:** 
  * Alice and Bob do not have a corresponding unique ID in `EmployeeUNI`, so we show `null` for them.
  * Meir, Winston, and Jonathan have their respective unique IDs matched.

---

#### 💡 Approach & Logic (MS SQL Server)
* Since we need to keep **all** employees from the `Employees` table even if they don't have a matching unique ID in `EmployeeUNI`, we use a **`LEFT JOIN`**.
* We start from the `Employees` table (`e`) and left join `EmployeeUNI` (`eu`) on their common column (`id`).
* If a match isn't found, MS SQL Server automatically assigns `NULL` to the `unique_id` column.

---

#### 💻 MS SQL Code
```sql
SELECT eu.unique_id, e.name
FROM Employees e
LEFT JOIN EmployeeUNI eu
  ON e.id = eu.id;
