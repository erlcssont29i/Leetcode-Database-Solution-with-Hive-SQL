# Hive Solution

```sql
SELECT 
  id, 
  month,
  sum(salary)over(partition by id order by month) as salary -- 累加金額
FROM
(select *,
row_number() over(partition by id order by month desc ) as rn
from leetcode.ex_579_employee ) a 
where rn > 1
order by id,month desc 
;
```
