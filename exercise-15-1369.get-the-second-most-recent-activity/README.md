# Exercise 15：1369.Get The Second Most Recent Activity

## 1.Description

Table: `UserActivity`

```
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| username      | varchar |
| activity      | varchar |
| startDate     | Date    |
| endDate       | Date    |
+---------------+---------+
This table does not contain primary key.
This table contain information about the activity performed of each user in a period of time.
A person with username performed a activity from startDate to endDate.
```

Write an SQL query to show the **second most recent activity** of each user.

If the user only has one activity, return that one.

A user can’t perform more than one activity at the same time. Return the result table in **any** order.

The query result format is in the following example:

```
UserActivity table:
+------------+--------------+-------------+-------------+
| username   | activity     | startDate   | endDate     |
+------------+--------------+-------------+-------------+
| Alice      | Travel       | 2020-02-12  | 2020-02-20  |
| Alice      | Dancing      | 2020-02-21  | 2020-02-23  |
| Alice      | Travel       | 2020-02-24  | 2020-02-28  |
| Bob        | Travel       | 2020-02-11  | 2020-02-18  |
+------------+--------------+-------------+-------------+

Result table:
+------------+--------------+-------------+-------------+
| username   | activity     | startDate   | endDate     |
+------------+--------------+-------------+-------------+
| Alice      | Dancing      | 2020-02-21  | 2020-02-23  |
| Bob        | Travel       | 2020-02-11  | 2020-02-18  |
+------------+--------------+-------------+-------------+

The most recent activity of Alice is Travel from 2020-02-24 to 2020-02-28, before that she was dancing from 2020-02-21 to 2020-02-23.
Bob only has one record, we just take that one.
```

## 2.Create Table and insert into values

```sql
create table if not exists leetcode.ex_1369_user_activity
(user_name	string ,
 activity	string, 
 start_date	date,
 end_date	date
) stored as orc ;

INSERT INTO table leetcode.ex_1369_user_activity VALUES
('Alice', 'Travel', '2020-02-12', '2020-02-20'),
('Alice', 'Dancing', '2020-02-21', '2020-02-23'),
('Alice', 'Travel', '2020-02-24', '2020-02-28'),
('Bob', 'Travel', '2020-02-11', '2020-02-18')
;
```

{% hint style="info" %}
"Bob only has one record, we just take that one"，Indicates that if the user has only one activity, do not participate in the logical judgment of Most Recent.



"Bob only has one record, we just take that one"，表示如果當user只有一個活動，則不要參與Most Recent的邏輯判段
{% endhint %}

