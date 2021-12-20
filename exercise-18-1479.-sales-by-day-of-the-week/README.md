# Exercise 18：1479. Sales by Day of the Week

## 1.Description

Table: `Orders`

```
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| order_id      | int     |
| customer_id   | int     |
| order_date    | date    | 
| item_id       | varchar |
| quantity      | int     |
+---------------+---------+
(ordered_id, item_id) is the primary key for this table.
This table contains information of the orders placed.
order_date is the date when item_id was ordered by the customer with id customer_id.
```

Table: `Items`

```
+---------------------+---------+
| Column Name         | Type    |
+---------------------+---------+
| item_id             | varchar |
| item_name           | varchar |
| item_category       | varchar |
+---------------------+---------+
item_id is the primary key for this table.
item_name is the name of the item.
item_category is the category of the item.
```

You are the business owner and would like to obtain a sales report for category items and day of the week.

Write an SQL query to report how many units in each category have been ordered on each **day of the week**.

Return the result table **ordered** by category.

The query result format is in the following example:

```
Orders table:
+------------+--------------+-------------+--------------+-------------+
| order_id   | customer_id  | order_date  | item_id      | quantity    |
+------------+--------------+-------------+--------------+-------------+
| 1          | 1            | 2020-06-01  | 1            | 10          |
| 2          | 1            | 2020-06-08  | 2            | 10          |
| 3          | 2            | 2020-06-02  | 1            | 5           |
| 4          | 3            | 2020-06-03  | 3            | 5           |
| 5          | 4            | 2020-06-04  | 4            | 1           |
| 6          | 4            | 2020-06-05  | 5            | 5           |
| 7          | 5            | 2020-06-05  | 1            | 10          |
| 8          | 5            | 2020-06-14  | 4            | 5           |
| 9          | 5            | 2020-06-21  | 3            | 5           |
+------------+--------------+-------------+--------------+-------------+

Items table:
+------------+----------------+---------------+
| item_id    | item_name      | item_category |
+------------+----------------+---------------+
| 1          | LC Alg. Book   | Book          |
| 2          | LC DB. Book    | Book          |
| 3          | LC SmarthPhone | Phone         |
| 4          | LC Phone 2020  | Phone         |
| 5          | LC SmartGlass  | Glasses       |
| 6          | LC T-Shirt XL  | T-Shirt       |
+------------+----------------+---------------+

Result table:
+------------+-----------+-----------+-----------+-----------+-----------+-----------+-----------+
| Category   | Monday    | Tuesday   | Wednesday | Thursday  | Friday    | Saturday  | Sunday    |
+------------+-----------+-----------+-----------+-----------+-----------+-----------+-----------+
| Book       | 20        | 5         | 0         | 0         | 10        | 0         | 0         |
| Glasses    | 0         | 0         | 0         | 0         | 5         | 0         | 0         |
| Phone      | 0         | 0         | 5         | 1         | 0         | 0         | 10        |
| T-Shirt    | 0         | 0         | 0         | 0         | 0         | 0         | 0         |
+------------+-----------+-----------+-----------+-----------+-----------+-----------+-----------+
On Monday (2020-06-01, 2020-06-08) were sold a total of 20 units (10 + 10) in the category Book (ids: 1, 2).
On Tuesday (2020-06-02) were sold a total of 5 units  in the category Book (ids: 1, 2).
On Wednesday (2020-06-03) were sold a total of 5 units in the category Phone (ids: 3, 4).
On Thursday (2020-06-04) were sold a total of 1 unit in the category Phone (ids: 3, 4).
On Friday (2020-06-05) were sold 10 units in the category Book (ids: 1, 2) and 5 units in Glasses (ids: 5).
On Saturday there are no items sold.
On Sunday (2020-06-14, 2020-06-21) were sold a total of 10 units (5 +5) in the category Phone (ids: 3, 4).
There are no sales of T-Shirt.
```

## 2.Create Table and insert into values

```sql
create table if not exists leetcode.ex_1479_orders
(order_id 	string, 
customer_id string,
order_date	date,
item_id			string,
quantity		int 
) stored as orc ;

INSERT INTO table leetcode.ex_1479_orders VALUES
('1','1','2020-06-01','1','10'),
('2','1','2020-06-08','2','10'),
('3','2','2020-06-02','1','5'),
('4','3','2020-06-03','3','5'), 
('5','4','2020-06-04','4','1'),
('6','4','2020-06-05','5','5'),
('7','5','2020-06-05','1','10'), 
('8','5','2020-06-14','4','5'), 
('9','5','2020-06-21','3','5') 
;
create table if not exists leetcode.ex_1479_items
(item_id				string,
 item_name			string,
 item_category	string
) stored as orc ;

INSERT INTO table leetcode.ex_1479_items VALUES
('1','LC Alg. Book','Book'),
('2','LC DB. Book','Book'),
('3','LC SmarthPhone','Phone'),
('4','LC Phone 2020','Phone'),
('5','LC SmartGlass','Glasses'),
('6','LC T-Shirt XL','T-Shirt') 
;
```

{% hint style="info" %}
There is no function for the day of the week in Hive (SQL is dayofweek()), but it can be implemented with datediff() and pmod()

```
方法：pmod(datediff('date', '2012-01-01'), 7)  
```

2012-01-01 is Sunday, the above function returns "0-6" ("0-6" means "Sunday-Saturday" respectively)



Ｈive中沒有內建星期幾的函數(SQL是`dayofweek()`)，可使用日期相减函数(`datediff()`)及取余函数`pmod()`配合實現

2012-01-01為星期日，上述函數返回值为“0-6”(“0-6”分别表示“星期日-星期六)
{% endhint %}

