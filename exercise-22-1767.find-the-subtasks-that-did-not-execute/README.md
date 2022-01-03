# Exercise 22：1767.Find the Subtasks That Did Not Execute

## 1.Description

Table: `Tasks`

```
+----------------+---------+
| Column Name    | Type    |
+----------------+---------+
| task_id        | int     |
| subtasks_count | int     |
+----------------+---------+
task_id is the primary key for this table.
Each row in this table indicates that task_id was divided into subtasks_count subtasks labelled from 1 to subtasks_count.
It is guaranteed that 2 <= subtasks_count <= 20.
```

Table: `Executed`

```
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| task_id       | int     |
| subtask_id    | int     |
+---------------+---------+
(task_id, subtask_id) is the primary key for this table.
Each row in this table indicates that for the task task_id, the subtask with ID subtask_id was executed successfully.
It is guaranteed that subtask_id <= subtasks_count for each task_id.
```

Write an SQL query to report the IDs of the missing subtasks for each `task_id`.

Return the result table in **any order**.

The query result format is in the following example:

```
Tasks table:
+---------+----------------+
| task_id | subtasks_count |
+---------+----------------+
| 1       | 3              |
| 2       | 2              |
| 3       | 4              |
+---------+----------------+

Executed table:
+---------+------------+
| task_id | subtask_id |
+---------+------------+
| 1       | 2          |
| 3       | 1          |
| 3       | 2          |
| 3       | 3          |
| 3       | 4          |
+---------+------------+

Result table:
+---------+------------+
| task_id | subtask_id |
+---------+------------+
| 1       | 1          |
| 1       | 3          |
| 2       | 1          |
| 2       | 2          |
+---------+------------+
Task 1 was divided into 3 subtasks (1, 2, 3). Only subtask 2 was executed successfully, so we include (1, 1) and (1, 3) in the answer.
Task 2 was divided into 2 subtasks (1, 2). No subtask was executed successfully, so we include (2, 1) and (2, 2) in the answer.
Task 3 was divided into 4 subtasks (1, 2, 3, 4). All of the subtasks were executed successfully.
```

## 2.Create Table and insert into values

```sql
create table if not exists leetcode.ex_1767_tasks
(task_id string, subtasks_count int) stored as orc ;

INSERT INTO table leetcode.ex_1767_tasks VALUES
('1','3'),
('2','2'),
('3','4') ; 

create table if not exists leetcode.ex_1767_executed
(task_id string , subtask_id string ) stored as orc ;

INSERT INTO table leetcode.ex_1767_executed VALUES
('1','2'),
('3','1'),
('3','2'),
('3','3'),
('3','4') ; 
```

{% hint style="info" %}
In SQL, we create an identity column to auto-generate incremental values by IDENTITY Function while this system function does not exist in Hive. We can create a UDF function([user-defined function](https://docs.cloudera.com/HDPDocuments/HDP3/HDP-3.0.0/using-hiveql/content/hive\_create\_udf.html)) .
{% endhint %}

