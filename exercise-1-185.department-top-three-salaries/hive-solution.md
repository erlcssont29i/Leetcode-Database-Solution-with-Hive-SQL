# Hive Solution

## 3.Hive Solution

```sql
SELECT t1.* FROM
(SELECT
b.id as department_id,
a.name,
a.salary,
dense_rank()OVER(partition by b.id order by a.salary desc ) as rank
-- row_number()OVER(partition by b.id order by a.salary desc ) as rank
FROM 
(select * from  leetcode.ex_185_employee)  a 
 left join (select * from  leetcode.ex_185_employee)  b ON a.department_id=b.id
 ) t1 WHERE t1.rank<=3
 ;
```

