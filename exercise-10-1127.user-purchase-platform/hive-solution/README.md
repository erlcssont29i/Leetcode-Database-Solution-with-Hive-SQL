# Hive Solution

## 3.Hive Solution

```sql
SELECT
    x.user_id,
    x.spend_date,
    x.platform,
    x.total_amount,
    count(x.user_id) as total_user
FROM
(
select 
    t1.user_id,
    t1.spend_date, 
    t2.mobile_amount,
    t3.desktop_amount,
    coalesce(mobile_amount,0)+coalesce(desktop_amount,0) as total_amount,
    case when mobile_amount is not null and desktop_amount is not null then 'both'
        when mobile_amount is not null and desktop_amount is null then 'mobile_only'
        when mobile_amount is  null and desktop_amount is not null then 'desktop_only'
       END as platform
-- select *
from 
    (select distinct  user_id,spend_date from ex_1127_spending) t1
    left join
    (select  user_id,spend_date,sum(amount) as mobile_amount
        from ex_1127_spending  
            where platform ='mobile'
            group by user_id,spend_date) t2 
                    ON t1.user_id=t2.user_id and t1.spend_date=t2.spend_date
    left  join 
    (select  user_id,spend_date,sum(amount) as desktop_amount
        from ex_1127_spending  
            where platform ='desktop'
            group by user_id,spend_date) t3 
                    ON t1.user_id=t3.user_id and t1.spend_date=t3.spend_date
) x 
GROUP BY x.user_id,x.spend_date, x.platform,x.total_amount 
;
```

