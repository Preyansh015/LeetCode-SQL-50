# 1280. Students and Examinations

<img src="https://img.shields.io/badge/Difficulty-Easy-brightgreen?style=flat-square" alt="Difficulty Easy"> 

## 📝 Problem Statement
Write a solution to find the number of times each student attended each exam.

Return the result table ordered by `student_id` and `subject_name`.

---

## 📋 Table Schema

**`Students` Table:**
| Column Name | Type | Description |
| :--- | :--- | :--- |
| `student_id` | int | Primary key representing student ID |
| `student_name` | varchar | Name of the student |

**`Subjects` Table:**
| Column Name | Type | Description |
| :--- | :--- | :--- |
| `subject_name` | varchar | Primary key representing subject name |

**`Examinations` Table:**
| Column Name | Type | Description |
| :--- | :--- | :--- |
| `student_id` | int | ID of the student attending the exam |
| `subject_name` | varchar | Name of the subject exam attended |

---

## 🔍 Examples

**Example 1:**

* **Input:** 
  * `Students` table:
    | student_id | student_name |
    | :---: | :--- |
    | 1 | Alice |
    | 2 | Bob |
    | 13 | John |
    | 6 | Alex |
  
  * `Subjects` table:
    | subject_name |
    | :--- |
    | Math |
    | Physics |
    | Programming |
  
  * `Examinations` table:
    | student_id | subject_name |
    | :---: | :--- |
    | 1 | Math |
    | 1 | Physics |
    | 1 | Programming |
    | 2 | Programming |
    | 1 | Physics |
    | 1 | Math |
    | 13 | Math |
    | 13 | Programming |
    | 13 | Physics |
    | 2 | Math |
    | 1 | Math |

* **Output:** 
  | student_id | student_name | subject_name | attended_exams |
  | :---: | :--- | :--- | :---: |
  | 1 | Alice | Math | 3 |
  | 1 | Alice | Physics | 2 |
  | 1 | Alice | Programming | 1 |
  | 2 | Bob | Math | 1 |
  | 2 | Bob | Physics | 0 |
  | 2 | Bob | Programming | 1 |
  | 6 | Alex | Math | 0 |
  | 6 | Alex | Physics | 0 |
  | 6 | Alex | Programming | 0 |
  | 13 | John | Math | 1 |
  | 13 | John | Physics | 1 |
  | 13 | John | Programming | 1 |

---

## 💡 Approach & Logic (MS SQL Server)
* Use a **`CROSS JOIN`** between `Students` and `Subjects` to generate every possible combination of student and subject (ensuring students who attended 0 exams still show up).
* Use a **`LEFT JOIN`** with the `Examinations` table on both `student_id` and `subject_name`.
* Group by `student_id`, `student_name`, and `subject_name`, and use `COUNT(e.subject_name)` to count the number of exam attendances (evaluating to `0` when no match exists).
* Order the final result by `student_id` and `subject_name`.

---

## 💻 MS SQL Code
```sql
SELECT s.student_id, s.student_name, sub.subject_name, COUNT(e.subject_name) AS attended_exams
FROM Students s
CROSS JOIN Subjects sub
LEFT JOIN Examinations e
  ON s.student_id = e.student_id
 AND sub.subject_name = e.subject_name
GROUP BY s.student_id, s.student_name, sub.subject_name
ORDER BY s.student_id, sub.subject_name;
