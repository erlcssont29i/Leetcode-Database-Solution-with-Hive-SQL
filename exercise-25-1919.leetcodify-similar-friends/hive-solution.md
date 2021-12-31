# Hive Solution

## 3.Hive Solution

```sql
SELECT 
    a.user_id,
    a.recommended_id 
FROM 
(select -- t1.*,t2.* from
     t1.user_id,
     t2.user_id as recommended_id,
     count(t2.song_id) as same_soung_cnt
from 
(select user_id ,song_id ,day 
    from leetcode.ex_1917_listens) t1
 join 
 (select user_id ,song_id ,day 
    from leetcode.ex_1917_listens) t2 
 		ON t1.user_id < t2.user_id and t1.song_id=t2.song_id and t1.day=t2.day 
 group by  t1.user_id,t2.user_id
 having same_soung_cnt>=3 ) a
left join
 (select user1_id,user2_id from leetcode.ex_1917_friendship ) b
    ON a.user_id =b.user1_id 
WHERE  a.recommended_id = b.user2_id -- change the join condition of the 1917 question
;
```

