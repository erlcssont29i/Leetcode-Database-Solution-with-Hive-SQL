# Hive Solution

## 3.Hive Solution

```sql
-- solution 1 

SELECT 
  id,visit_date,people 
FROM 
(select * ,id+2 as c1,lead(id,2,id+2)over(order by id ) as c2
 from ex_601_stadium
  where people >= 100) a 
 where c1=c2 ; 

-- solution 2 

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

