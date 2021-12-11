# Hive Solution

```sql
SELECT -- * ,
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

