# Hive Solution

## 3.Hive Solution

```sql
SELECT a.* FROM
(select *,
 count()OVER (PARTITION BY company) cnt,
 row_number()OVER (PARTITION BY company ORDER BY salary) as rn 
from leetcode.ex_569_employee) a 
 where rn between cnt/2 and (cnt/2)+1  
 ; 
```

