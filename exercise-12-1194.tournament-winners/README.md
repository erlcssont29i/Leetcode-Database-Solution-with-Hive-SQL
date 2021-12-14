# Exercise 12：1194.Tournament Winners

## 1.Description

Table: `Players`

```
+-------------+-------+
| Column Name | Type  |
+-------------+-------+
| player_id   | int   |
| group_id    | int   |
+-------------+-------+
player_id is the primary key of this table.
Each row of this table indicates the group of each player
```

Table: `Matches`

```
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| match_id      | int     |
| first_player  | int     |
| second_player | int     | 
| first_score   | int     |
| second_score  | int     |
+---------------+---------+
- match_id is the primary key of this table.
- Each row is a record of a match, first_player and second_player 
contain the player_id of each match.
- first_score and second_score contain the number of points of the first_player 
and second_player respectively.
- You may assume that, in each match, players belongs to the same group.

```

The winner in each group is the player who scored the maximum total points within the group. In the case of a tie, the **lowest** player\_id wins.

Write an SQL query to find the winner in each group.

The query result format is in the following example:

```
Players table:
+-----------+------------+
| player_id | group_id   |
+-----------+------------+
| 15        | 1          |
| 25        | 1          |
| 30        | 1          |
| 45        | 1          |
| 10        | 2          |
| 35        | 2          |
| 50        | 2          |
| 20        | 3          |
| 40        | 3          |
+-----------+------------+

Matches table:
+------------+--------------+---------------+-------------+--------------+
| match_id   | first_player | second_player | first_score | second_score |
+------------+--------------+---------------+-------------+--------------+
| 1          | 15           | 45            | 3           | 0            |
| 2          | 30           | 25            | 1           | 2            |
| 3          | 30           | 15            | 2           | 0            |
| 4          | 40           | 20            | 5           | 2            |
| 5          | 35           | 50            | 1           | 1            |
+------------+--------------+---------------+-------------+--------------+

Result table:
+-----------+------------+
| group_id  | player_id  |
+-----------+------------+ 
| 1         | 15         |
| 2         | 35         |
| 3         | 40         |
+-----------+------------+
```

## 2.Create Table and insert into values

```sql
create table if not exists leetcode.ex_1194_players
(player_id	string ,group_id	string) stored as orc ;

INSERT INTO table leetcode.ex_1194_players VALUES
('15', '1'),          
('25', '1'),          
('30', '1'),          
('45', '1'),          
('10', '2'),          
('35', '2'),          
('50', '2'),          
('20', '3'),          
('40', '3')
;

create table if not exists leetcode.ex_1194_matches
(match_id				string, 
 first_player 	string,
 second_player 	string,
 first_score		int,
 second_score		int
) stored as orc ;

INSERT INTO table leetcode.ex_1194_matches VALUES
('1', '15', '45', '3', '0'),  
('2', '30', '25', '1', '2'),  
('3', '30', '15', '2', '0'),  
('4', '40', '20', '5', '2'), 
('5', '35', '50', '1', '1')        
```

{% hint style="info" %}
Test how to use UNION and Window Function, pay attention to the type of UNION
{% endhint %}

