# Hive Solution

## 3.Hive Solution

```sql
SELECT
x.group_id,x.player_id
FROM
(SELECT
t2.group_id,t1.player_id,score_ttl,
row_number()OVER(partition by t2.group_id order by t1.score_ttl desc,t1.player_id ) as rn
FROM
  (select 
   	player_id,
   	sum(score) as score_ttl
  from 
  	(select first_player as player_id,first_score as score from leetcode.ex_1194_matches
  	UNION ALL
  	select second_player as player_id, second_score as score from leetcode.ex_1194_matches ) a 
group by player_id
	) t1
 join (select player_id,group_id from ex_1194_players) t2 ON t1.player_id=t2.player_id
) x
WHERE x.rn=1 
;
```

