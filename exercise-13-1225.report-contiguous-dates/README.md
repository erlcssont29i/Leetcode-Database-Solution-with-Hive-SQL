# Exercise 13：1225.Report Contiguous Dates

## 1.Description

Table: `Failed`

```
+--------------+---------+
| Column Name  | Type    |
+--------------+---------+
| fail_date    | date    |
+--------------+---------+
Primary key for this table is fail_date.
Failed table contains the days of failed tasks.
```

Table: `Succeeded`

```
+--------------+---------+
| Column Name  | Type    |
+--------------+---------+
| success_date | date    |
+--------------+---------+
Primary key for this table is success_date.
Succeeded table contains the days of succeeded tasks.
```

A system is running one task **every day**. Every task is independent of the previous tasks. The tasks can fail or succeed.

Write an SQL query to generate a report of `period_state` for each continuous interval of days in the period from **2019-01-01** to **2019-12-31**.

`period_state` is ‘_failed_’ if tasks in this interval failed or ‘_succeeded_’ if tasks in this interval succeeded. Interval of days are retrieved as `start_date` and `end_date`.

Order result by `start_date`.

The query result format is in the following example:

```
Failed table:
+-------------------+
| fail_date         |
+-------------------+
| 2018-12-28        |
| 2018-12-29        |
| 2019-01-04        |
| 2019-01-05        |
+-------------------+

Succeeded table:
+-------------------+
| success_date      |
+-------------------+
| 2018-12-30        |
| 2018-12-31        |
| 2019-01-01        |
| 2019-01-02        |
| 2019-01-03        |
| 2019-01-06        |
+-------------------+


Result table:
+--------------+--------------+--------------+
| period_state | start_date   | end_date     |
+--------------+--------------+--------------+
| succeeded    | 2019-01-01   | 2019-01-03   |
| failed       | 2019-01-04   | 2019-01-05   |
| succeeded    | 2019-01-06   | 2019-01-06   |
+--------------+--------------+--------------+

The report ignored the system state in 2018 as we care about the system in the period 2019-01-01 to 2019-12-31.
From 2019-01-01 to 2019-01-03 all tasks succeeded and the system state was "succeeded".
From 2019-01-04 to 2019-01-05 all tasks failed and system state was "failed".
From 2019-01-06 to 2019-01-06 all tasks succeeded and system state was "succeeded"

```

## 2.Create Table and insert into values

```sql
create table if not exists leetcode.ex_1125_failed
(fail_date	date) stored as orc ;

INSERT INTO table leetcode.ex_1125_failed VALUES
('2018-12-28'), 
('2018-12-29'), 
('2019-01-04'), 
('2019-01-05') ; 

create table if not exists leetcode.ex_1125_succeeded
(success_date	date) stored as orc ;

INSERT INTO table leetcode.ex_1125_succeeded VALUES
('2018-12-30'), 
('2018-12-31'), 
('2019-01-01'), 
('2019-01-02'), 
('2019-01-03'), 
('2019-01-06') ;
```

{% hint style="info" %}
要以狀態(成功/失敗)+<mark style="color:blue;">**"?"**</mark>(某個不存在的字段)作為一個分組對象，難點在如何創造出?字段
{% endhint %}

