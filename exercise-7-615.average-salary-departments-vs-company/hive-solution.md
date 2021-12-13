# Hive Solution

## 3.Hive Solution

```sql
SELECT 
t1.pay_month,
t1.department_id,
case when department_avg > company_avg then 'higher' 
	when department_avg = company_avg then 'same'
	when department_avg < company_avg then 'lower'
 end as comparison
FROM
(select 
substr(pay_date,1,7) as pay_month,
department_id,
avg(amount) as department_avg
from 
(select * from ex_615_salary ) a
join (select * from ex_615_employee) b ON a.employee_id=b.employee_id
group by pay_date,department_id ) t1 -- 部門
join 
(select substr(pay_date,1,7) as pay_month,
 	avg(amount) as company_avg 
 from ex_615_salary group by substr(pay_date,1,7) ) t2 -- 公司
 ON t1.pay_month =t2.pay_month
 order by t1.pay_month DESC
;
```

