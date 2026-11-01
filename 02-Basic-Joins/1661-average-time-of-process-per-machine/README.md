# 1661. Average Time of Process per Machine

<img src="https://img.shields.io/badge/Difficulty-Easy-brightgreen?style=flat-square" alt="Difficulty Easy"> 

## 📝 Problem Statement
There is a factory website that has several machines, each running one or more processes. Write a solution to find the average time each machine takes to complete a process.

The time to complete a process is the `'end'` timestamp minus the `'start'` timestamp. The average time is calculated by the total time to complete every process on the machine divided by the number of processes that were run on that machine.

The resulting table should have the `machine_id` along with the average time as `processing_time`, which should be rounded to 3 decimal places.

Return the result table in any order.

---

## 📋 Table Schema: `Activity`
| Column Name | Type | Description |
| :--- | :--- | :--- |
| `machine_id` | int | ID of the machine |
| `process_id` | int | ID of the process running on the machine |
| `activity_type` | enum | Type of activity (`'start'` or `'end'`) |
| `timestamp` | float | Current time in seconds |

* `(machine_id, process_id, activity_type)` is the primary key.
* The `start` timestamp is always less than or equal to the `end` timestamp for every `(machine_id, process_id)` pair.

---

## 🔍 Examples

**Example 1:**

* **Input:** `Activity` table
  
  | machine_id | process_id | activity_type | timestamp |
  | :---: | :---: | :---: | :---: |
  | 0 | 0 | start | 0.712 |
  | 0 | 0 | end | 1.520 |
  | 0 | 1 | start | 3.140 |
  | 0 | 1 | end | 4.120 |
  | 1 | 0 | start | 0.550 |
  | 1 | 0 | end | 1.550 |
  | 1 | 1 | start | 0.430 |
  | 1 | 1 | end | 1.420 |
  | 2 | 0 | start | 4.100 |
  | 2 | 0 | end | 4.512 |
  | 2 | 1 | start | 2.500 |
  | 2 | 1 | end | 5.000 |

* **Output:** 
  
  | machine_id | processing_time |
  | :---: | :---: |
  | 0 | 0.894 |
  | 1 | 0.995 |
  | 2 | 1.456 |

* **Explanation:** 
  * Machine 0's average time: `((1.520 - 0.712) + (4.120 - 3.140)) / 2 = 0.894`
  * Machine 1's average time: `((1.550 - 0.550) + (1.420 - 0.430)) / 2 = 0.995`
  * Machine 2's average time: `((4.512 - 4.100) + (5.000 - 2.500)) / 2 = 1.456`

---

## 💡 Approach & Logic (MS SQL Server)
* Perform a **Self-Join** on the `Activity` table where `a1` represents the `'start'` event and `a2` represents the `'end'` event for the exact same `machine_id` and `process_id`.
* Calculate the difference between the end and start timestamps (`a2.timestamp - a1.timestamp`) for each process.
* Group by `machine_id` and apply the `AVG()` aggregate function.
* Use `ROUND(..., 3)` to format the final processing time to 3 decimal places.

---

## 💻 MS SQL Code
```sql
SELECT a1.machine_id, ROUND(AVG(a2.timestamp - a1.timestamp), 3) AS processing_time
FROM Activity a1 
JOIN Activity a2 
  ON a1.machine_id = a2.machine_id 
 AND a1.process_id = a2.process_id 
 AND a1.activity_type = 'start' 
 AND a2.activity_type = 'end'
GROUP BY a1.machine_id;
