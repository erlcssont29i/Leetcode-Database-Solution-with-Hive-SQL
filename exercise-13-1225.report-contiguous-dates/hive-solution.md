# Hive Solution

## 3.Hive Solution

```sql
SELECT 
  x.period_state, -- x.rank_parti-ran,
  min(x.ymd) as start_date,
  max(x.ymd) as end_date
FROM
  (SELECT 
  a.period_state,a.ymd,
  row_number()OVER(partition by a.period_state order by a.ymd ) as rank_parti,
  row_number()OVER(order by a.ymd ) as rank
  FROM
      (select 'failed' as period_state,fail_date as ymd 
      from leetcode.ex_1225_failed
        where year(fail_date)='2019'
      union all 
      select 'succeeded' as period_state,success_date as ymd 
      from  leetcode.ex_1225_succeeded
        where year(success_date)='2019') a 
  ) x  
  GROUP BY x.period_state,x.rank_parti-rank
  ORDER BY x.start_date 
;
```

