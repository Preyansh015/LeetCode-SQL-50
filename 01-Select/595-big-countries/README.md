---

### 595. Big Countries
<img src="https://img.shields.io/badge/Difficulty-Easy-brightgreen?style=flat-square" alt="Difficulty Easy"> 

#### 📝 Problem Statement
A country is big if:
* It has an area of at least three million (i.e., `3000000 km²`), or
* It has a population of at least twenty-five million (i.e., `25000000`).

Write a solution to find the name, population, and area of the big countries.

Return the result table in any order.

---

#### 📋 Table Schema: `World`
| Column Name | Type | Description |
| :--- | :--- | :--- |
| `name` | varchar | Primary key (unique values) representing the country name |
| `continent` | varchar | Continent the country belongs to |
| `area` | int | Total area in km² |
| `population` | int | Total population |
| `gdp` | bigint | Gross Domestic Product |

---

#### 🔍 Examples

**Example 1:**

* **Input:** `World` table
  
  | name | continent | area | population | gdp |
  | :---: | :---: | :---: | :---: | :---: |
  | Afghanistan | Asia | 652230 | 25500100 | 20343000000 |
  | Albania | Europe | 28748 | 2831741 | 12960000000 |
  | Algeria | Africa | 2381741 | 37100000 | 188681000000 |
  | Andorra | Europe | 468 | 78115 | 3712000000 |
  | Angola | Africa | 1246700 | 20609294 | 100990000000 |

* **Output:** 
  
  | name | population | area |
  | :---: | :---: | :---: |
  | Afghanistan | 25500100 | 652230 |
  | Algeria | 37100000 | 2381741 |

* **Explanation:** 
  * Afghanistan has a population of `25,500,100` (which is `>= 25,000,000`), making it a big country.
  * Algeria has a population of `37,100,000` (which is `>= 25,000,000`), making it a big country.

---

#### 💡 Approach & Logic (MS SQL Server)
* Select the required columns: `name`, `population`, and `area`.
* Use the `WHERE` clause combined with the logical `OR` operator to check if either condition is met (`area >= 3000000` or `population >= 25000000`).

---

#### 💻 MS SQL Code
```sql
SELECT name, population, area
FROM World
WHERE area >= 3000000
   OR population >= 25000000;
