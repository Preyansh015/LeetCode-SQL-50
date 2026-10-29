# 1068. Product Sales Analysis I

<img src="https://img.shields.io/badge/Difficulty-Easy-brightgreen?style=flat-square" alt="Difficulty Easy"> 

## 📝 Problem Statement
Write a solution to report the `product_name`, `year`, and `price` for each `sale_id` in the `Sales` table.

Return the resulting table in any order.

---

## 📋 Table Schema

**`Sales` Table:**
| Column Name | Type | Description |
| :--- | :--- | :--- |
| `sale_id` | int | Sale ID (`sale_id`, `year` is primary key) |
| `product_id` | int | Foreign key to Product table |
| `year` | int | Year of sale |
| `quantity` | int | Quantity sold |
| `price` | int | Price per unit |

**`Product` Table:**
| Column Name | Type | Description |
| :--- | :--- | :--- |
| `product_id` | int | Primary key representing product ID |
| `product_name` | varchar | Name of the product |

---

## 🔍 Examples

**Example 1:**

* **Input:** 
  * `Sales` table:
    | sale_id | product_id | year | quantity | price |
    | :---: | :---: | :---: | :---: | :---: |
    | 1 | 100 | 2008 | 10 | 5000 |
    | 2 | 100 | 2009 | 12 | 5000 |
    | 7 | 200 | 2011 | 15 | 9000 |
  
  * `Product` table:
    | product_id | product_name |
    | :---: | :--- |
    | 100 | Nokia |
    | 200 | Apple |
    | 300 | Samsung |

* **Output:** 
  | product_name | year | price |
  | :--- | :---: | :---: |
  | Nokia | 2008 | 5000 |
  | Nokia | 2009 | 5000 |
  | Apple | 2011 | 9000 |

* **Explanation:** 
  * From `sale_id = 1`, product `100` corresponds to Nokia, sold in 2008 for 5000.
  * From `sale_id = 2`, product `100` corresponds to Nokia, sold in 2009 for 5000.
  * From `sale_id = 7`, product `200` corresponds to Apple, sold in 2011 for 9000.

---

## 💡 Approach & Logic (MS SQL Server)
* Use an `INNER JOIN` (or `JOIN`) between the `Product` table and the `Sales` table on the matching `product_id` column.
* Select the required columns: `product_name` from the Product table, and `year` and `price` from the Sales table.

---

## 💻 MS SQL Code
```sql
SELECT p.product_name, s.year, s.price
FROM Product p
JOIN Sales s
  ON p.product_id = s.product_id;
