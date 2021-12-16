# Exercise 10：1127.User Purchase Platform

## 1.Description

Table: `Spending`

```
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| user_id     | int     |
| spend_date  | date    |
| platform    | enum    |
| amount      | int     |
+-------------+---------+
The table logs the spendings history of users that make purchases from an online shopping website which has a desktop and a mobile application.
(user_id, spend_date, platform) is the primary key of this table.
The platform column is an ENUM type of ('desktop', 'mobile').
```

Write an SQL query to find the total number of users and the total amount spent using mobile **only**, desktop **only** and **both** mobile and desktop together for each date.

The query result format is in the following example:

```
Spending table:
+---------+------------+----------+--------+
| user_id | spend_date | platform | amount |
+---------+------------+----------+--------+
| 1       | 2019-07-01 | mobile   | 100    |
| 1       | 2019-07-01 | desktop  | 100    |
| 2       | 2019-07-01 | mobile   | 100    |
| 2       | 2019-07-02 | mobile   | 100    |
| 3       | 2019-07-01 | desktop  | 100    |
| 3       | 2019-07-02 | desktop  | 100    |
+---------+------------+----------+--------+

Result table:
+------------+----------+--------------+-------------+
| spend_date | platform | total_amount | total_users |
+------------+----------+--------------+-------------+
| 2019-07-01 | desktop  | 100          | 1           |
| 2019-07-01 | mobile   | 100          | 1           |
| 2019-07-01 | both     | 200          | 1           |
| 2019-07-02 | desktop  | 100          | 1           |
| 2019-07-02 | mobile   | 100          | 1           |
| 2019-07-02 | both     | 0            | 0           |
+------------+----------+--------------+-------------+
On 2019-07-01, user 1 purchased using both desktop and mobile, user 2 purchased using mobile only and user 3 purchased using desktop only.
On 2019-07-02, user 2 purchased using mobile only, user 3 purchased using desktop only and no one purchased using both platforms.
```

## 2.Create Table and insert into values

```sql
create table if not exists leetcode.ex_1127_spending
(user_id	string, 
 spend_date date,
 platform	string,
 amount int ) stored as orc ;

INSERT INTO table leetcode.ex_1127_spending  VALUES
('1'       ,'2019-07-01' ,'mobile'   ,'100'),
('1'       ,'2019-07-01' ,'desktop'  ,'100'),
('2'       ,'2019-07-01' ,'mobile'   ,'100'),
('2'       ,'2019-07-02' ,'mobile'   ,'100'),
('3'       ,'2019-07-01' ,'desktop'  ,'100'),
('3'       ,'2019-07-02' ,'desktop'  ,'100')
```

> 難點：如何判斷出一個user是否同時在兩平台都有購買(即platform=both)

## 3.Hive Solution

```sql
SELECT
    x.user_id,
    x.spend_date,
    x.platform,
    x.total_amount,
    count(x.user_id) as total_user
FROM
(
select 
    t1.user_id,
    t1.spend_date, 
    t2.mobile_amount,
    t3.desktop_amount,
    coalesce(mobile_amount,0)+coalesce(desktop_amount,0) as total_amount,
    case when mobile_amount is not null and desktop_amount is not null then 'both'
        when mobile_amount is not null and desktop_amount is null then 'mobile_only'
        when mobile_amount is  null and desktop_amount is not null then 'desktop_only'
       END as platform
-- select *
from 
    (select distinct  user_id,spend_date from ex_1127_spending) t1
    left join
    (select  user_id,spend_date,sum(amount) as mobile_amount
        from ex_1127_spending  
            where platform ='mobile'
            group by user_id,spend_date) t2 
                    ON t1.user_id=t2.user_id and t1.spend_date=t2.spend_date
    left  join 
    (select  user_id,spend_date,sum(amount) as desktop_amount
        from ex_1127_spending  
            where platform ='desktop'
            group by user_id,spend_date) t3 
                    ON t1.user_id=t3.user_id and t1.spend_date=t3.spend_date
) x 
GROUP BY x.user_id,x.spend_date, x.platform,x.total_amount 
;
```
