# Hive Solution

## 3.Hive Solution

```sql
SELECT 
t1.user_id as seller_id,
CASE WHEN t1.favorite_brand =t2.item_brand then 'yes'
 ELSE 'no' END as 2nd_item_fav_brand
FROM
(select user_id,favorite_brand from  leetcode.ex_1159_user) t1 
LEFT JOIN  
 (
   select  a.seller_id,a.order_date,a.item_id,a.rn,b.item_brand
    from 
    (select seller_id,order_date,item_id,
        row_number()over(partition by seller_id order by order_date) as rn
        from leetcode.ex_1159_orders ) a 
     join (select item_id,item_brand from  leetcode.ex_1159_items) b on a.item_id=b.item_id
   where rn=2
) t2 ON t1.user_id=t2.seller_id
;
```

