# Hive Solution

## 3.Hive Solution

```sql
SELECT
request_at,
round(count(if(status='cancelled_by_driver',id,NULL))/count(id),2) as cancel_rate
-- a.*,b.client_is_bannd,b.driver_is_bannd
FROM
(select  * from leetcode.ex_262_trips 
    where status <> 'cancelled_by_client') a 
join 
(select * from leetcode.ex_262_users 
 where role='client'
  and banned ='No') b ON a.client_id=b.users_id
join  
(select * from leetcode.ex_262_users 
 where role='driver'
  and banned ='No') c ON a.driver_id=c.users_id
 group by request_at
 ;
```

