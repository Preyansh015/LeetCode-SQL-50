---

### 1148. Article Views I
<img src="https://img.shields.io/badge/Difficulty-Easy-brightgreen?style=flat-square" alt="Difficulty Easy"> 

#### 📝 Problem Statement
Write a solution to find all the authors that viewed at least one of their own articles.

Return the result table sorted by id in ascending order.

---

#### 📋 Table Schema: `Views`
| Column Name | Type | Description |
| :--- | :--- | :--- |
| `article_id` | int | ID of the article |
| `author_id` | int | ID of the author who wrote the article |
| `viewer_id` | int | ID of the user who viewed the article |
| `view_date` | date | Date of the view |

* There is no primary key for this table; it may contain duplicate rows.
* Equal `author_id` and `viewer_id` indicate the same person (author viewing their own article).

---

#### 🔍 Examples

**Example 1:**

* **Input:** `Views` table
  
  | article_id | author_id | viewer_id | view_date |
  | :---: | :---: | :---: | :---: |
  | 1 | 3 | 5 | 2019-08-01 |
  | 1 | 3 | 6 | 2019-08-02 |
  | 2 | 7 | 7 | 2019-08-01 |
  | 2 | 7 | 6 | 2019-08-02 |
  | 4 | 7 | 1 | 2019-07-22 |
  | 3 | 4 | 4 | 2019-07-21 |
  | 3 | 4 | 4 | 2019-07-21 |

* **Output:** 
  
  | id |
  | :---: |
  | 4 |
  | 7 |

* **Explanation:** 
  * Author 7 viewed their own article (article_id: 2, viewer_id: 7).
  * Author 4 viewed their own article twice (article_id: 3, viewer_id: 4).

---

#### 💡 Approach & Logic (MS SQL Server)
* Filter the rows where `author_id` equals `viewer_id` to catch instances where authors viewed their own work.
* Use `DISTINCT` to remove duplicate IDs since an author might view their own article multiple times.
* Use `ORDER BY id ASC` to sort the results as requested.

---

#### 💻 MS SQL Code
```sql
SELECT DISTINCT author_id AS id
FROM Views
WHERE author_id = viewer_id
ORDER BY id ASC;
