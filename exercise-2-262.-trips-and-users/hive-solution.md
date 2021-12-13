# Hive Solution

## 3.Hive Solution

```sql
SELECT
a.*,b.client_is_bannd,b.driver_is_bannd
FROM
(select  * from leetcode.ex_262_trips) a 
left join 
(select * from leetcode.ex_262_users 
 where role='client') b ON a.client_id=b.user_id
left join  
(select * from leetcode.ex_262_users 
 where role='driver') c ON a.driver_id=c.user_id
 ;
```

