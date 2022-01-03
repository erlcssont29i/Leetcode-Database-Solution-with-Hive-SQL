# Hive Solution

## 3.Hive Solution

```sql
SELECT id  
-- select *,
-- cast(next1 as int)-cast(id as int ) , 
-- cast(next2 as int)-cast(id as int ) 
FROM 
(select *,
   lead(id,1,id+1)over(order by visit_date) as next1,
   lead(id,2,id+2)over(order by visit_date) as next2
from leetcode.ex_601_stadium where people>=100 ) a 
    where cast(next1 as int)-cast(id as int ) = 1  
        and cast(next2 as int)-cast(id as int ) = 2
    ;
```

