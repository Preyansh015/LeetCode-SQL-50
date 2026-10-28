---

### 1683. Invalid Tweets
<img src="https://img.shields.io/badge/Difficulty-Easy-brightgreen?style=flat-square" alt="Difficulty Easy"> 

#### 📝 Problem Statement
Write a solution to find the IDs of the invalid tweets. A tweet is invalid if the number of characters used in the content of the tweet is strictly greater than 15.

Return the result table in any order.

---

#### 📋 Table Schema: `Tweets`
| Column Name | Type | Description |
| :--- | :--- | :--- |
| `tweet_id` | int | Primary key (unique values) representing the tweet ID |
| `content` | varchar | The text content of the tweet |

---

#### 🔍 Examples

**Example 1:**

* **Input:** `Tweets` table
  
  | tweet_id | content |
  | :---: | :--- |
  | 1 | Let us Code |
  | 2 | More than fifteen chars are here! |

* **Output:** 
  
  | tweet_id |
  | :---: |
  | 2 |

* **Explanation:** 
  * Tweet 1 has length = 11 (Valid tweet).
  * Tweet 2 has length = 33 (Invalid tweet since length > 15).

---

#### 💡 Approach & Logic (MS SQL Server)
* Use the built-in MS SQL function `LEN(content)` to calculate the character length of each tweet's content.
* Apply a `WHERE` clause to filter out rows where the length is strictly greater than 15 (`> 15`).

---

#### 💻 MS SQL Code
```sql
SELECT tweet_id
FROM Tweets
WHERE LEN(content) > 15;
