# Hive Solution

## 3.Hive Solution

```sql
SELECT 
  user1_id,
  friend_like_page,
  count(user1_friend) as friends_likes
  -- t1.user1_id,
  -- t1.user1_friend,
  -- t1.friend_like_page
  -- t2.page_id as friend_and_me_both_like_page
FROM
(select 
  a.user1_id, 
  a.user2_id as user1_friend ,
	b.page_id as friend_like_page
 from
(select user1_id,user2_id from leetcode.ex_1892_friendship
  union -- can NOT use UNION ALL!
select user2_id as user1_id ,user1_id as user2_id from leetcode.ex_1892_friendship
	) a 
join (select * from leetcode.ex_1892_likes) b ON a.user2_id=b.user_id
) t1 -- * my freind like-page list

LEFT JOIN 
(select * from leetcode.ex_1892_likes) t2 
    ON t1.user1_id = t2.user_id 
    and  t1.friend_like_page = t2.page_id 
      -- ** check is my friend's like-page same with me 
WHERE  t2.page_id is null 
group by user1_id,friend_like_page
;
```

