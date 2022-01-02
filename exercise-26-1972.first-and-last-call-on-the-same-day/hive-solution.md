# Hive Solution

## 3.Hive Solution

```sql
SELECT x.user_id FROM
(
select distinct user_id  
from 
(select user_id,call_day,call_time , 
	dense_rank()over(partition by call_day order by call_time ) as rn 
from 
(select caller_id as user_id,to_date(call_time) as call_day, call_time from leetcode.ex_1972_calls
    union all 
select recipient_id as user_id,to_date(call_time) as call_day, call_time from leetcode.ex_1972_calls
	) a 
	  ) t1 where rn = 1 
    		) x 
INNER JOIN 
(
select distinct user_id 
from 
(select user_id,call_day,call_time , 
	dense_rank()over(partition by call_day order by call_time desc) as rn_desc
from 
(select caller_id as user_id,to_date(call_time) as call_day, call_time from leetcode.ex_1972_calls
    union all 
select recipient_id as user_id,to_date(call_time) as call_day, call_time from leetcode.ex_1972_calls
	) a 
	  ) t2 where rn_desc = 1 
    		) y ON x.user_id= y.user_id
;
```

