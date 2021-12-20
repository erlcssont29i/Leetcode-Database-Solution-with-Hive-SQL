# Hive Solution

## 3.Hive Solution

```sql
SELECT 
  a.item_category,
  sum(if(b.day_of_week=1 ,b.quantity,0)) as monday,
  sum(if(b.day_of_week=2 ,b.quantity,0)) as tuesday,
  sum(if(b.day_of_week=3 ,b.quantity,0)) as wednesday,
  sum(if(b.day_of_week=4 ,b.quantity,0)) as thursday,
  sum(if(b.day_of_week=5 ,b.quantity,0)) as friday,
  sum(if(b.day_of_week=6 ,b.quantity,0)) as saturday,
  sum(if(b.day_of_week=0 ,b.quantity,0)) as sunday
fROM
(select * from leetcode.ex_1479_items) a 
left join 
(select *, pmod(datediff(order_date, '2012-01-01'), 7)  as day_of_week 
 	from leetcode.ex_1479_orders) b ON a.item_id=b.item_id
group by a.item_category
;
```

