# Hive Solution

## 3.Hive Solution

```sql
SELECT america,asia,europ
FROM 
(select name as america ,row_number()over() as id from leetcode.ex_618_student 
 	where continent = 'America' order by America) a 
full join 
(select name as asia ,row_number()over() as id from leetcode.ex_618_student 
 	where continent = 'Asia' order by Asia) b on a.id=b.id
full join 
(select name as europe ,row_number()over() as id from leetcode.ex_618_student 
 	where continent = 'Europe' order by Europe) c on a.id=c.id
 	;
```

