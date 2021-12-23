# Hive Solution

## 3.Hive Solution

```sql
SELECT 
    substr(x.yyyymm,6,2) as mm,
    round((dis1+dis2+dis3)/3,2) as average_ride_distance ,
    round((dur1+dur2+dur3)/3,2) as average_ride_duration
FROM
(
SELECT  
	t0.yyyymm,
	coalesce(t1.ride_distance,0) as dis1,
	coalesce(lead(t1.ride_distance,1)over(order by t0.yyyymm),0) as dis2,
	coalesce(lead(t1.ride_distance,2)over(order by t0.yyyymm),0) as dis3,
	coalesce(t1.ride_duration,0) as dur1,
	coalesce(lead(t1.ride_duration,1)over(order by t0.yyyymm),0) as dur2,
	coalesce(lead(t1.ride_duration,2)over(order by t0.yyyymm),0) as dur3
FROM  
  ( select '2020-01' as yyyymm
    union select '2020-02' as yyyymm
    union select '2020-03' as yyyymm
    union select '2020-04' as yyyymm
    union select '2020-05' as yyyymm
    union select '2020-06' as yyyymm
    union select '2020-07' as yyyymm
    union select '2020-08' as yyyymm
    union select '2020-09' as yyyymm
    union select '2020-10' as yyyymm
   -- union select '2020-11' as yyyymm
   -- union select '2020-12' as yyyymm  
    ) t0
left join
(
select substr(b.requested_at,1,7) as requested_month ,
  coalesce(sum(a.ride_distance) ,0) as ride_distance,
  coalesce(sum(a.ride_duration) ,0) as ride_duration
from 
(select * from leetcode.ex_1635_acceptedrides ) a 
		join (select * from leetcode.ex_1635_rides ) b ON  a.ride_id=b.ride_id 
  group by substr(b.requested_at,1,7)  
 ) t1 ON t0.yyyymm =t1.requested_month
  	) x 
  	;
```

