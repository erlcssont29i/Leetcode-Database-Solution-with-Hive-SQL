# Exercise 7：615.Average Salary: Departments VS Company

## 1.Description

Given two tables as below, write a query to display the comparison result (higher/lower/same) of the average salary of employees in a department to the company’s average salary.

Table: salary

```
| id | employee_id | amount | pay_date   |
|----|-------------|--------|------------|
| 1  | 1           | 9000   | 2017-03-31 |
| 2  | 2           | 6000   | 2017-03-31 |
| 3  | 3           | 10000  | 2017-03-31 |
| 4  | 1           | 7000   | 2017-02-28 |
| 5  | 2           | 6000   | 2017-02-28 |
| 6  | 3           | 8000   | 2017-02-28 |
```

The employee\_id column refers to the employee\_id in the following table employee.

```
| employee_id | department_id |
|-------------|---------------|
| 1           | 1             |
| 2           | 2             |
| 3           | 2             |
```

So for the sample data above, the result is:

```
| pay_month | department_id | comparison  |
|-----------|---------------|-------------|
| 2017-03   | 1             | higher      |
| 2017-03   | 2             | lower       |
| 2017-02   | 1             | same        |
| 2017-02   | 2             | same        |
```

## 2.Create Table and insert into values

```sql
create table if not exists leetcode.ex_615_salary
(
  id 						string,
  employee_id		string,
  amount 				int,
  pay_date 			date
) stored as orc ;
INSERT INTO table leetcode.ex_615_salary  VALUES
('1'  ,'1'   ,'9000'   , '2017-03-31' ),
('2'  ,'2'   ,'6000'   , '2017-03-31' ),
('3'  ,'3'   ,'10000'  , '2017-03-31' ),
('4'  ,'1'   ,'7000'   , '2017-02-28' ),
('5'  ,'2'   ,'6000'   , '2017-02-28' ),
('6'  ,'3'   ,'8000'   , '2017-02-28' )


create table if not exists leetcode.ex_615_employee
(employee_id	string, department_id	string) stored as orc ;
INSERT INTO table leetcode.ex_615_employee  VALUES
('1'   ,'1'),  ('2'   ,'2'), ('3'   ,'2')             
```

