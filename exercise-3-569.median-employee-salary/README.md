# Exercise 3：569.Median Employee Salary

## 1 Description

The `Employee` table holds all employees. The employee table has three columns: Employee Id, Company Name, and Salary.

```
+-----+------------+--------+
|Id   | Company    | Salary |
+-----+------------+--------+
|1    | A          | 2341   |
|2    | A          | 341    |
|3    | A          | 15     |
|4    | A          | 15314  |
|5    | A          | 451    |
|6    | A          | 513    |
|7    | B          | 15     |
|8    | B          | 13     |
|9    | B          | 1154   |
|10   | B          | 1345   |
|11   | B          | 1221   |
|12   | B          | 234    |
|13   | C          | 2345   |
|14   | C          | 2645   |
|15   | C          | 2645   |
|16   | C          | 2652   |
|17   | C          | 65     |
+-----+------------+--------+
```

Write a SQL query to find the median salary of each company. Bonus points if you can solve it without using any built-in SQL functions.

```
+-----+------------+--------+
|Id   | Company    | Salary |
+-----+------------+--------+
|5    | A          | 451    |
|6    | A          | 513    |
|12   | B          | 234    |
|9    | B          | 1154   |
|14   | C          | 2645   |
+-----+------------+--------+
```

## 2 Create Table and insert into values

```sql
create table if not exists leetcode.ex_569_employee
(
 id string, 
 company string, 
 salary int
)  stored as orc ;

INSERT INTO table leetcode.ex_569_employee  VALUES
('1'    ,'A'          ,'2341'   ),
('2'    ,'A'          ,'341'    ),
('3'    ,'A'          ,'15'     ),
('4'    ,'A'          ,'15314'  ),
('5'    ,'A'          ,'451'    ),
('6'    ,'A'          ,'513'    ),
('7'    ,'B'          ,'15'     ),
('8'    ,'B'          ,'13'     ),
('9'    ,'B'          ,'1154'   ),
('10'   ,'B'          ,'1345'   ),
('11'   ,'B'          ,'1221'   ),
('12'   ,'B'          ,'234'   	),
('13'   ,'C'          ,'2345'   ),
('14'   ,'C'          ,'2645'   ),
('15'   ,'C'          ,'2645'   ),
('16'   ,'C'          ,'2652'   ),
('17'   ,'C'          ,'65'     )

```

{% hint style="info" %}
In statistics and probability theory, the _median_ is the value separating the higher half from the lower half of a data sample. The _Median_ is the "middle" of a sorted list of numbers.

This problem requires we find which employee's salary is median and what salary is for each company, **NOT calculating the company's median salary.**
{% endhint %}



