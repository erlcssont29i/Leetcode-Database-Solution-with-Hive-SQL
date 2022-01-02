# Exercise 16：1384.Total Sales Amount by Year

## 1.Description

Table: `Product`

```
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| product_id    | int     |
| product_name  | varchar |
+---------------+---------+
product_id is the primary key for this table.
product_name is the name of the product.
```

Table: `Sales`

```
+---------------------+---------+
| Column Name         | Type    |
+---------------------+---------+
| product_id          | int     |
| period_start        | varchar |
| period_end          | date    |
| average_daily_sales | int     |
+---------------------+---------+
product_id is the primary key for this table. 
period_start and period_end indicates the start and end date for sales period, both dates are inclusive.
The average_daily_sales column holds the average daily sales amount of the items for the period.
```

Write an SQL query to report the Total sales amount of each item for each year, with corresponding product name, product\_id, product\_name and report\_year.

Dates of the sales years are between 2018 to 2020. Return the result table **ordered** by product\_id and report\_year.

The query result format is in the following example:

```
Product table:
+------------+--------------+
| product_id | product_name |
+------------+--------------+
| 1          | LC Phone     |
| 2          | LC T-Shirt   |
| 3          | LC Keychain  |
+------------+--------------+

Sales table:
+------------+--------------+-------------+---------------------+
| product_id | period_start | period_end  | average_daily_sales |
+------------+--------------+-------------+---------------------+
| 1          | 2019-01-25   | 2019-02-28  | 100                 |
| 2          | 2018-12-01   | 2020-01-01  | 10                  |
| 3          | 2019-12-01   | 2020-01-31  | 1                   |
+------------+--------------+-------------+---------------------+

Result table:
+------------+--------------+-------------+--------------+
| product_id | product_name | report_year | total_amount |
+------------+--------------+-------------+--------------+
| 1          | LC Phone     |    2019     | 3500         |
| 2          | LC T-Shirt   |    2018     | 310          |
| 2          | LC T-Shirt   |    2019     | 3650         |
| 2          | LC T-Shirt   |    2020     | 10           |
| 3          | LC Keychain  |    2019     | 31           |
| 3          | LC Keychain  |    2020     | 31           |
+------------+--------------+-------------+--------------+
LC Phone was sold for the period of 2019-01-25 to 2019-02-28, and there are 35 days for this period. Total amount 35*100 = 3500. 
LC T-shirt was sold for the period of 2018-12-01 to 2020-01-01, and there are 31, 365, 1 days for years 2018, 2019 and 2020 respectively.
LC Keychain was sold for the period of 2019-12-01 to 2020-01-31, and there are 31, 31 days for years 2019 and 2020 respectively.
```

## 2.Create Table and insert into values

```sql
create table if not exists leetcode.ex_1384_product
(product_id string, product_name string) stored as orc ;

INSERT INTO table leetcode.ex_1384_product VALUES
('1','LC Phone'),('2','LC T-Shirt'),('3','LC Keychain') ;

create table if not exists leetcode.ex_1384_sales
(product_id string,
 period_start	date, 
 period_end	date,
 average_daily_sales  int
) stored as orc ;

INSERT INTO table leetcode.ex_1384_sales VALUES
('1','2019-01-25','2019-02-28','100'), 
('2','2018-12-01','2020-01-01','10'),  
('3','2019-12-01','2020-01-31','1')    
;
```

