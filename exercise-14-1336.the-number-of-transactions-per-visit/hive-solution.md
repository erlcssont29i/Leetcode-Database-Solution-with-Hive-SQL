# Hive Solution

## 3.Hive Solution

```sql
select 
    coalesce(tran_cou,0) as tran_cou,
    sum(vis_cou) as vis_cou
from
(select user_id, visit_date,count(*) as vis_cou 
from leetcode.ex_1336_visits 
group by user_id,visit_date) a 
left join 
(select user_id,transaction_date,count(*) as tran_cou 
from leetcode.ex_1336_transactions  
group by user_id,transaction_date )b
    on a.user_id=b.user_id and a.visit_date=b.transaction_date
GROUP BY coalesce(tran_cou,0)
;
```

