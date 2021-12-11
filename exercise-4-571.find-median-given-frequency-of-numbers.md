# Exercise 4：571.Find Median Given Frequency of Numbers

## 4.1 Description

TThe `Numbers` table keeps the value of number and its frequency.

```
+----------+-------------+
|  Number  |  Frequency  |
+----------+-------------|
|  0       |  7          |
|  1       |  1          |
|  2       |  3          |
|  3       |  1          |
+----------+-------------+
```

In this table, the numbers are `0, 0, 0, 0, 0, 0, 0, 1, 2, 2, 2, 3`, so the median is `(0 + 0) / 2 = 0`.

```
+--------+
| median |
+--------|
| 0.0000 |
+--------+
```

Write a query to find the median of all numbers and name the result as `median`.

## 4.2 Hive Solution

```sql
create table if not exists leetcode.ex_571_number
(
 number int, 
 frequency int
)  stored as orc ;

INSERT INTO table leetcode.ex_571_number  VALUES
('0' , '7' ),
('1' , '1' ),
('2' , '3' ),
('3' , '1' )

-- hive answer
SELECT -- * 
	avg(number)
FROM
(select
number,frequency,
sum(frequency)OVER(order by number  ) as cumu_freq,
sum(frequency)OVER() as sum_freq
 from leetcode.ex_571_number ) a 
 --  order by number
 where cumu_freq between sum_freq/2 and (sum_freq/2)+1
 ;
```
