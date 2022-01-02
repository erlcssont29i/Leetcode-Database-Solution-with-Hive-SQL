# Hive Solution

## 3.Hive Solution

```sql
-- **Example 1:**

create table leetcode.ex_2004_s1 as 
SELECT 
    employee_id,
    experience,
    salary,
    salary_sum,
    (70000 - salary_sum) as balance  
FROM
(select *,sum(salary)over(ORDER BY rn) as salary_sum 
from  (select *, ROW_NUMBER() OVER( ORDER BY salary) AS rn from leetcode.ex_2004_candidates_1
 where experience  = 'Senior' ) a
 ) b 
 ;

create table leetcode.ex_2004_j1 as 
SELECT 
    t1.employee_id,
    t1.experience,
    t1.salary,
    t1.salary_sum,
    (t2.balance_min_senior - t1.salary_sum) as balance 
FROM 
( select 'id' as id,*,sum(salary)over(ORDER BY rn) as salary_sum
from (select *, ROW_NUMBER() OVER(ORDER BY salary) AS rn from leetcode.ex_2004_candidates_1
 where experience  = 'Junior' ) a 
 ) t1
 join (select 'id' as id, min(balance) as balance_min_senior from leetcode.ex_2004_s 
        where balance>0 ) t2  ON t1.id=t2.id 
;
    
    
select experience,count(employee_id) as accepted_candidates 
    from leetcode.ex_2004_s1 where balance>=0 
        group by experience
UNION
select  experience,count(employee_id) as accepted_candidates 
    from leetcode.ex_2004_j1 where balance>=0
        group by experience
        ;


-- **Example 2:**
create table leetcode.ex_2004_s2 as 
SELECT 
    employee_id,
    experience,
    salary,
    salary_sum,
    (70000 - salary_sum) as balance, 
FROM
(select *,sum(salary)over(ORDER BY rn) as salary_sum 
from  (select *, ROW_NUMBER() OVER( ORDER BY salary) AS rn from leetcode.ex_2004_candidates_2
 where experience  = 'Senior' ) a
 ) b 
 ;
 select * from leetcode.ex_2004_s2;

create table leetcode.ex_2004_j2 as 
SELECT 
    t1.employee_id,
    t1.experience,
    t1.salary,
    t1.salary_sum,
    (t2.balance_min_senior - t1.salary_sum) as balance 
FROM 
( select 'id' as id,*,sum(salary)over(ORDER BY rn) as salary_sum
from (select *, ROW_NUMBER() OVER(ORDER BY salary) AS rn from leetcode.ex_2004_candidates_2
 where experience  = 'Junior' ) a 
 ) t1
 join (select 'id' as id, coalesce(min(balance),70000) as balance_min_senior from leetcode.ex_2004_s2 
       where balance >0 
        ) t2  ON t1.id=t2.id 
    ;
 

select 'Senior' as experience,coalesce(count(employee_id),0) as accepted_candidates 
    from leetcode.ex_2004_s2 where balance>=0 
UNION
select 'Junior' as experience,coalesce(count(employee_id),0) as accepted_candidates 
    from leetcode.ex_2004_j2 where balance>=0
        ;
```

