# Exercise 17：1412.Find the Quiet Students in All Exams

## 1.Description

Table: `Student`

```
+---------------------+---------+
| Column Name         | Type    |
+---------------------+---------+
| student_id          | int     |
| student_name        | varchar |
+---------------------+---------+
student_id is the primary key for this table.
student_name is the name of the student.
```

Table: `Exam`

```
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| exam_id       | int     |
| student_id    | int     |
| score         | int     |
+---------------+---------+
(exam_id, student_id) is the primary key for this table.
Student with student_id got score points in exam with id exam_id.
```

A “quite” student is the one who took at least one exam and didn’t score neither the high score nor the low score.

Write an SQL query to report the students (student_id, student_name) being “quiet” in **ALL** exams.

Don’t return the student who has never taken any exam. Return the result table ordered by student\_id.

The query result format is in the following example.

```
Student table:
+-------------+---------------+
| student_id  | student_name  |
+-------------+---------------+
| 1           | Daniel        |
| 2           | Jade          |
| 3           | Stella        |
| 4           | Jonathan      |
| 5           | Will          |
+-------------+---------------+

Exam table:
+------------+--------------+-----------+
| exam_id    | student_id   | score     |
+------------+--------------+-----------+
| 10         |     1        |    70     |
| 10         |     2        |    80     |
| 10         |     3        |    90     |
| 20         |     1        |    80     |
| 30         |     1        |    70     |
| 30         |     3        |    80     |
| 30         |     4        |    90     |
| 40         |     1        |    60     |
| 40         |     2        |    70     |
| 40         |     4        |    80     |
+------------+--------------+-----------+

Result table:
+-------------+---------------+
| student_id  | student_name  |
+-------------+---------------+
| 2           | Jade          |
+-------------+---------------+

For exam 1: Student 1 and 3 hold the lowest and high score respectively.
For exam 2: Student 1 hold both highest and lowest score.
For exam 3 and 4: Studnet 1 and 4 hold the lowest and high score respectively.
Student 2 and 5 have never got the highest or lowest in any of the exam.
Since student 5 is not taking any exam, he is excluded from the result.
So, we only return the information of Student 2.
```

## 2.Create Table and insert into values

```sql
create table if not exists leetcode.ex_1412_student
(student_id string, student_name string) stored as orc ;

INSERT INTO table leetcode.ex_1412_student VALUES
('1','Daniel'), 
('2','Jade'), 
('3','Stella'),
('4','Jonathan'), 
('5','Will') 
;

create table if not exists leetcode.ex_1412_exam
(exam_id string, student_id string, score int) stored as orc ;

INSERT INTO table leetcode.ex_1412_exam VALUES
('10','1','70'), 
('10','2','80'), 
('10','3','90'), 
('20','1','80'), 
('30','1','70'), 
('30','3','80'),
('30','4','90'),
('40','1','60'),
('40','2','70'),
('40','4','80')
;
```

{% hint style="info" %}
“quite” student didn’t score neither the high score nor the low score.

&#x20;It's meams for each exam, we must find those students whose sort by scores are not equal to 1 in either ascending and  descending.
{% endhint %}

