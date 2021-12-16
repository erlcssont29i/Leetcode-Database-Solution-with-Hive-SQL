# Hive Solution

## 3.Hive Solution

```sql
SELECT 
	x.user_name,
	x.activity,
	x.start_date,
	x.end_date
FROM 
(select a.*, b.activity_cou,
 row_number()over(partition by a.user_name order by a.datediff DESC ) as rn
from 
  (select *, datediff(end_date,start_date) as datediff 
   		from leetcode.ex_1369_user_activity) a 
  left join 
  (select user_name,count(activity) as activity_cou -- 只有1個活動的用戶不參與題目要求的判斷
   		from  leetcode.ex_1369_user_activity
  				group by user_name) b ON a.user_name=b.user_name
) x
WHERE x.activity_cou =1 or (x.activity_cou>1 and x.rn=2)
;
```

