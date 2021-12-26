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

{% hint style="success" %}
`row_number(),rank()`和`dense_rank()`都是用來排序的函數，差异主要在排序的順序。`row_number()`不管排名是否有相同的，都按照順序1，2，3…..n、`rank()`排名相同的名次一樣，同一排名有幾個，後面排名就會跳過幾次、`dense_rank()`排名相同的名次一樣，且後面名次不跳號。

* The `ROW_NUMBER()` window function determines the ordinal number of the current row within its partition. The ORDER BY expression in the OVER clause determines the number. Each value is ordered within its partition. Rows with equal values for the ORDER BY expressions receive different row numbers nondeterministically.
* The `RANK()` window function determines the rank of a value in a group of values. The ORDER BY expression in the OVER clause determines the value. Each value is ranked within its partition. Rows with equal values for the ranking criteria receive the same rank. Drill adds the number of tied rows to the tied rank to calculate the next rank and thus the ranks might not be consecutive numbers. For example, if two rows are ranked 1, the next rank is 3. The DENSE\_RANK window function differs in that no gaps exist if two or more rows tie.
* The `DENSE_RANK()` window function determines the rank of a value in a group of values based on the ORDER BY expression and the OVER clause. Each value is ranked within its partition. Rows with equal values receive the same rank. There are no gaps in the sequence of ranked values if two or more rows have the same rank.
{% endhint %}
