# Hive Solution

## 3.Hive Solution

```sql
SELECT
    product_id,
    product_name,
    report_year,
    total_amount
FROM
(
 select 
 a.product_id,product_name,'2018' as report_year,
CASE when year(period_start)='2018' and  year(period_end)='2018' 
        then  average_daily_sales*(datediff(period_end,period_start)+1)
     when year(period_start)='2018' and year(period_end)>'2018' 
        then average_daily_sales*(datediff('2018-12-31',period_start)+1) 
    when year(period_start)<'2018' and year(period_end)='2018' 
        then average_daily_sales*(datediff(period_end,'2018-01-01')+1) 
    when year(period_start)<'2018' and year(period_end)>'2018' 
        then average_daily_sales*365
    END as total_amount
from 
(select * from leetcode.ex_1384_sales) a 
join 
(select * from leetcode.ex_1384_product) b on a.product_id=b.product_id

UNION ALL
  
 select 
 a.product_id,product_name,'2019' as report_year,
CASE when year(period_start)='2019' and  year(period_end)='2019' 
        then  average_daily_sales*(datediff(period_end,period_start)+1)
     when year(period_start)='2019' and year(period_end)>'2019' 
        then average_daily_sales*(datediff('2019-12-31',period_start)+1) 
    when year(period_start)<'2019' and year(period_end)='2019' 
        then average_daily_sales*(datediff(period_end,'2019-01-01')+1) 
    when year(period_start)<'2019' and year(period_end)>'2019' 
        then average_daily_sales*365
    END as total_amount
from 
(select * from leetcode.ex_1384_sales) a 
join 
(select * from leetcode.ex_1384_product) b on a.product_id=b.product_id

UNION ALL
 
 select 
 a.product_id,product_name,'2020' as report_year,
CASE when year(period_start)='2020' and  year(period_end)='2020' 
        then  average_daily_sales*(datediff(period_end,period_start)+1)
     when year(period_start)='2020' and year(period_end)>'2020' 
        then average_daily_sales*(datediff('2020-12-31',period_start)+1) 
    when year(period_start)<'2020' and year(period_end)='2020' 
        then average_daily_sales*(datediff(period_end,'2020-01-01')+1) 
    when year(period_start)<'2020' and year(period_end)>'2020' 
        then average_daily_sales*365
    END as total_amount
from 
(select * from leetcode.ex_1384_sales) a 
join 
(select * from leetcode.ex_1384_product) b on a.product_id=b.product_id
		) x 
			WHERE total_amount is NOT NULL
;
```

