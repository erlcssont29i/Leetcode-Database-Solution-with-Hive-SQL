# Exercise 1：185.Department Top Three Salaries

## 1 Description

Table: `Employee`

```
+--------------+---------+
| Column Name  | Type    |
+--------------+---------+
| id           | int     |
| name         | varchar |
| salary       | int     |
| departmentId | int     |
+--------------+---------+
id is the primary key column for this table.
departmentId is a foreign key of the ID from the Department table.
Each row of this table indicates the ID, name, and salary of an employee. It also contains the ID of their department.
```

Table: `Department`

```
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| id          | int     |
| name        | varchar |
+-------------+---------+
id is the primary key column for this table.
Each row of this table indicates the ID of a department and its name.
```

A company's executives are interested in seeing who earns the most money in each of the company's departments. A **high earner** in a department is an employee who has a salary in the **top three unique** salaries for that department.

Write an SQL query to find the employees who are **high earners** in each of the departments.

Return the result table **in any order**.

The query result format is in the following example.

**Example 1:**

```
Input: 
Employee table:
+----+-------+--------+--------------+
| id | name  | salary | departmentId |
+----+-------+--------+--------------+
| 1  | Joe   | 85000  | 1            |
| 2  | Henry | 80000  | 2            |
| 3  | Sam   | 60000  | 2            |
| 4  | Max   | 90000  | 1            |
| 5  | Janet | 69000  | 1            |
| 6  | Randy | 85000  | 1            |
| 7  | Will  | 70000  | 1            |
+----+-------+--------+--------------+
Department table:
+----+-------+
| id | name  |
+----+-------+
| 1  | IT    |
| 2  | Sales |
+----+-------+
Output: 
+------------+----------+--------+
| Department | Employee | Salary |
+------------+----------+--------+
| IT         | Max      | 90000  |
| IT         | Joe      | 85000  |
| IT         | Randy    | 85000  |
| IT         | Will     | 70000  |
| Sales      | Henry    | 80000  |
| Sales      | Sam      | 60000  |
+------------+----------+--------+
Explanation: 
In the IT department:
- Max earns the highest unique salary
- Both Randy and Joe earn the second-highest unique salary
- Will earns the third-highest unique salary

In the Sales department:
- Henry earns the highest salary
- Sam earns the second-highest salary
- There is no third-highest salary as there are only two employees
```

## 2 Create Table and insert into values

```sql
 -- create table and insert into values
create table if not exists leetcode.ex_185_employee
(
 id string,
 name	string,
 salary int,
 department_id string
) comment '員工表' stored as orc ;

INSERT INTO table leetcode.ex_185_employee  VALUES
('1'  , 'Joe'   , 85000  , '1'),
('2'  , 'Henry' , 80000  , '2'),
('3'  , 'Sam'   , 60000  , '2'),
('4'  , 'Max'   , 90000  , '1'),
('5'  , 'Janet' , 69000  , '1'),
('6'  , 'Randy' , 85000  , '1'),
('7'  , 'Will'  , 70000  , '1')  

create table if not exists leetcode.ex_185_department
(id	string, 
 name	string
) comment '部門表'  stored as orc ;

INSERT INTO table leetcode.ex_185_department VALUES
('1'  , 'IT'   ),
('2'  , 'Sales')

```

{% hint style="info" %}
According to the exercise's description, we have to think about using the ranking window function. (Because window functions operate on a set of rows and return a single value for each row from the underlying query)

Pay attention to the return result, it requires the **top three unique** salaries for that department but returns 4 data for the IT department, which means that the rank is the same for the same salary.&#x20;
{% endhint %}

