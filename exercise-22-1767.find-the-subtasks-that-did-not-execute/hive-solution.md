# Hive Solution

## 3.Hive Solution

```sql
SELECT 
		x.task_id,
		x.subtask_id
FROM
(
select t1.task_id,t2.subtask_id 
 from 
  (select * from  leetcode.ex_1767_tasks ) t1
  join(
  select 1 as subtask_id 
  union select 2 as subtask_id 
  union select 3 as subtask_id 
  union select 4 as subtask_id 
	) t2 ON t1.subtasks_count >= t2.subtask_id
)  x 
left join 
 (select task_id, ubtask_id from leetcode.ex_1767_executed ) y 
 					ON x.task_id= y.task_id and x.subtask_id=y.subtask_id
WHERE y.subtask_id is NULL
ORDER BY x.task_id,x.subtask_id
;
```

