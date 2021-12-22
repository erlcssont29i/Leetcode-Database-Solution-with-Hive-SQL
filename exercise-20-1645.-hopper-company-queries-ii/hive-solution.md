# Hive Solution

## 3.Hive Solution

```sql
set hive.strict.checks.cartesian.product=flase;
set hive.mapred.mode=nonstrict;

SELECT
    substr(x.yyyymm,6,2) as mm,
    -- x.active_drivers,
    -- coalesce(y.accepted_rides,0) as accepted_rides
    round((coalesce(y.accepted_rides,0)/x.active_drivers)*100,2) as  working_percentage
FROM 
(
 select 
   t0.yyyymm, 
   sum(coalesce(t1.active_drivers)) as  active_drivers
from  
  (select '2020-01' as yyyymm
    union select '2020-02' as yyyymm
    union select '2020-03' as yyyymm
    union select '2020-04' as yyyymm
    union select '2020-05' as yyyymm
    union select '2020-06' as yyyymm
    union select '2020-07' as yyyymm
    union select '2020-08' as yyyymm
    union select '2020-09' as yyyymm
    union select '2020-10' as yyyymm
    union select '2020-11' as yyyymm
    union select '2020-12' as yyyymm  
    ) t0
left join 
(select 
    substr(join_date,1,7) as join_month,
    count(driver_id) as active_drivers
from leetcode.ex_1635_drivers
  group by  substr(join_date,1,7)  ) t1 ON t0.yyyymm >= t1. join_month
group by t0.yyyymm 
	) x 
LEFT JOIN 
(
select 
  substr(b.requested_at,1,7) as requested_month,
  count (a.ride_id) as accepted_rides
from 
(select * from leetcode.ex_1635_acceptedrides ) a 
join (select * from leetcode.ex_1635_rides) b ON a.ride_id=b.ride_id 
	group by substr(b.requested_at,1,7)
) y ON x.yyyymm =y.requested_month 
;
```

