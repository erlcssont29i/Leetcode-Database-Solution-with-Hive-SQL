# Hive Solution

## 3.Hive Solution

```sql
SELECT 
  x.student_id,
  x.student_name
FROM 
(
select 
  t1.student_id,t1.student_name,
  sum(if( t1.rn=1 or t1.rn_desc = 1 , 1 ,0 )) as is_not_quite
from 
(select 
  a.student_id, a.student_name,b.exam_id,
  row_number()over(partition by b.exam_id order by b.score desc ) as rn_desc,
  row_number()over(partition by b.exam_id order by b.score ) as rn
from 
(select student_id, student_name from  leetcode.ex_1412_student) a
join 
(select exam_id,student_id,score from  leetcode.ex_1412_exam ) b 
    ON a.student_id=b.student_id ) t1   
group by t1.student_id,t1.student_name 
) x WHERE x.is_not_quite= 0
;
```

