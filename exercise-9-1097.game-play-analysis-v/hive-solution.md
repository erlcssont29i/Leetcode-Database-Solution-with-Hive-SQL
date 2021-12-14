# Hive Solution

## 3.Hive Solution

```sql
-- Thinking1:每個player_id最小的act日期為註冊日
-- Thinking2:每個player_id註冊日的下一個event_date為註冊日期+1，即是day1_retention

-- ## solution1
SELECT 
a.install_dt,
count(a.player_id) as installs,
count(if( date_add(a.install_dt,1) = b.event_date_next,a.player_id,null)) 
	as reten_player,
count(if( date_add(a.install_dt,1) = b.event_date_next,a.player_id,null))
	/count(a.player_id) as day1_retention
FROM  
(select player_id, min(event_date) as install_dt
    from leetcode.ex_1097_activity group by player_id) a 
left join  
(select player_id, event_date,
	lead(event_date)over(partition by player_id order by event_date) 
	    as event_date_next
		from leetcode.ex_1097_activity) b 
	    ON a.player_id=b.player_id 
		and a.install_dt=b.event_date
GROUP BY a.install_dt ; 

	
	
-- ## solution2
SELECT 
a.install_dt,
count(a.player_id) as installs ,
count(b.event_date)/count(a.player_id) as day1_retention
FROM 
(select player_id, min(event_date) as install_dt
    from leetcode.ex_1097_activity group by player_id) a 
 left join 
 (select player_id,event_date from leetcode.ex_1097_activity) b 
 			ON a.player_id=b.player_id 
       				and date_add(install_dt,1)=event_date
 GROUP BY a.install_dt ;
```

