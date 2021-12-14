# Exercise 8：618.Students Report By Geography

## 1.Description

A U.S graduate school has students from Asia, Europe and America. The students' location information are stored in table `student` as below.

```
| name   | continent |
|--------|-----------|
| Jack   | America   |
| Pascal | Europe    |
| Xi     | Asia      |
| Jane   | America   |
```

Pivot the continent column in this table so that each name is sorted alphabetically and displayed underneath its corresponding continent. The output headers should be America, Asia and Europe respectively. It is guaranteed that the student number from America is no less than either Asia or Europe.

For the sample input, the output is:

```
| America | Asia | Europe |
|---------|------|--------|
| Jack    | Xi   | Pascal |
| Jane    |      |        |
```

## 2.Create Table and insert into values

```sql
create table if not exists leetcode.ex_618_student
(name	string, continent	string ) stored as orc ;

INSERT INTO table leetcode.ex_618_student  VALUES
('Jack'   , 'America'),
('Pascal' , 'Europe'),
('Xi'     , 'Asia'),
('Jane'   , 'America')
```

