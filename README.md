# SQLhomework1Joins

mysql> INSERT INTO Table1 (ID, Value)
    -> SELECT 1, 'First'
    -> UNION ALL
    -> SELECT 2, 'Second'
    -> UNION ALL
    -> SELECT 3, 'Third'
    -> UNION ALL
    -> SELECT 4, 'Fourth'
    -> UNION ALL
    -> SELECT 5, 'Fifth';
Query OK, 5 rows affected (0.02 sec)

mysql> select * from table1;
+------+--------+
| ID   | Value  |
+------+--------+
|    1 | First  |
|    2 | Second |
|    3 | Third  |
|    4 | Fourth |
|    5 | Fifth  |
+------+--------+
5 rows in set (0.00 sec)

mysql> CREATE TABLE table2
    -> (ID INT,Value VARCHAR(10));
Query OK, 0 rows affected (0.02 sec)

mysql> INSERT INTO Table2 (ID, Value)
    -> SELECT 1, 'First'
    -> UNION ALL
    -> SELECT 2, 'Second'
    -> UNION ALL
    -> SELECT 3, 'Third'
    -> UNION ALL
    -> SELECT 6, 'Sixth'
    -> UNION ALL
    -> SELECT 7, 'Seventh'
    -> UNION ALL
    -> SELECT 8, 'Eighth';
Query OK, 6 rows affected (0.01 sec)
Records: 6  Duplicates: 0  Warnings: 0

mysql> select * from table2;
+------+---------+
| ID   | Value   |
+------+---------+
|    1 | First   |
|    2 | Second  |
|    3 | Third   |
|    6 | Sixth   |
|    7 | Seventh |
|    8 | Eighth  |
+------+---------+
6 rows in set (0.00 sec)

mysql> SELECT t1.*, t2.*
    -> FROM Table1 t1
    -> INNER JOIN Table2 t2 ON t1.ID = t2.ID;
+------+--------+------+--------+
| ID   | Value  | ID   | Value  |
+------+--------+------+--------+
|    1 | First  |    1 | First  |
|    2 | Second |    2 | Second |
|    3 | Third  |    3 | Third  |
+------+--------+------+--------+
3 rows in set (0.00 sec)

mysql> SELECT t1.ID AS T1ID, t1.Value AS T1Value,
    -> t2.ID AS T2ID, t2.Value AS T2Value
    -> FROM Table1 t1
    -> CROSS JOIN Table2 t2;
+------+---------+------+---------+
| T1ID | T1Value | T2ID | T2Value |
+------+---------+------+---------+
|    5 | Fifth   |    1 | First   |
|    4 | Fourth  |    1 | First   |
|    3 | Third   |    1 | First   |
|    2 | Second  |    1 | First   |
|    1 | First   |    1 | First   |
|    5 | Fifth   |    2 | Second  |
|    4 | Fourth  |    2 | Second  |
|    3 | Third   |    2 | Second  |
|    2 | Second  |    2 | Second  |
|    1 | First   |    2 | Second  |
|    5 | Fifth   |    3 | Third   |
|    4 | Fourth  |    3 | Third   |
|    3 | Third   |    3 | Third   |
|    2 | Second  |    3 | Third   |
|    1 | First   |    3 | Third   |
|    5 | Fifth   |    6 | Sixth   |
|    4 | Fourth  |    6 | Sixth   |
|    3 | Third   |    6 | Sixth   |
|    2 | Second  |    6 | Sixth   |
|    1 | First   |    6 | Sixth   |
|    5 | Fifth   |    7 | Seventh |
|    4 | Fourth  |    7 | Seventh |
|    3 | Third   |    7 | Seventh |
|    2 | Second  |    7 | Seventh |
|    1 | First   |    7 | Seventh |
|    5 | Fifth   |    8 | Eighth  |
|    4 | Fourth  |    8 | Eighth  |
|    3 | Third   |    8 | Eighth  |
|    2 | Second  |    8 | Eighth  |
|    1 | First   |    8 | Eighth  |
+------+---------+------+---------+

mysql> CREATE TABLE Employee(
    -> EmployeeID INT PRIMARY KEY,
    -> Name NVARCHAR(50),
    -> ManagerID INT
    -> );
Query OK, 0 rows affected, 1 warning (0.02 sec)

mysql> INSERT INTO Employee
    -> SELECT 1, 'Mike', 3
    -> UNION ALL
    -> SELECT 2, 'David', 3
    -> UNION ALL
    -> SELECT 3, 'Roger', NULL
    -> UNION ALL
    -> SELECT 4, 'Marry', 2
    -> UNION ALL
    -> SELECT 5, 'Joseph', 2
    -> UNION ALL
    -> SELECT 7, 'Ben', 2;
Query OK, 6 rows affected (0.01 sec)
Records: 6  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM Employee;
+------------+--------+-----------+
| EmployeeID | Name   | ManagerID |
+------------+--------+-----------+
|          1 | Mike   |         3 |
|          2 | David  |         3 |
|          3 | Roger  |      NULL |
|          4 | Marry  |         2 |
|          5 | Joseph |         2 |
|          7 | Ben    |         2 |
+------------+--------+-----------+
6 rows in set (0.00 sec)

mysql> SELECT e1.Name EmployeeName, e2.name AS ManagerName
    -> FROM Employee e1
    -> INNER JOIN Employee e2
    -> ON e1.ManagerID = e2.EmployeeID;
+--------------+-------------+
| EmployeeName | ManagerName |
+--------------+-------------+
| Mike         | Roger       |
| David        | Roger       |
| Marry        | David       |
| Joseph       | David       |
| Ben          | David       |
+--------------+-------------+
5 rows in set (0.00 sec)

mysql> SELECT e1.Name EmployeeName, IFNULL(e2.name, 'Top Manager') AS ManagerName
    -> FROM Employee e1
    -> LEFT JOIN Employee e2
    -> ON e1.ManagerID = e2.EmployeeID;
+--------------+-------------+
| EmployeeName | ManagerName |
+--------------+-------------+
| Mike         | Roger       |
| David        | Roger       |
| Roger        | Top Manager |
| Marry        | David       |
| Joseph       | David       |
| Ben          | David       |
+--------------+-------------+
6 rows in set (0.00 sec)

mysql> SELECT t1.ID AS T1ID, t1.Value1 AS T1Value,
    -> t2.ID T2ID, t2.Value2 AS T2Value
    -> FROM Table1 t1
    -> NATURAL JOIN Table2 t2;
+------+---------+------+---------+
| T1ID | T1Value | T2ID | T2Value |
+------+---------+------+---------+
|    1 | First   |    1 | First   |
|    2 | Second  |    2 | Second  |
|    3 | Third   |    3 | Third   |
+------+---------+------+---------+
3 rows in set (0.00 sec)

mysql> SELECT t1.ID T1ID, t1.Value1 AS T1Value
    -> FROM Table1 t1
    -> UNION
    -> SELECT t2.ID AS T2ID, t2.Value2 AS T2Value
    -> FROM Table2 t2;
+------+---------+
| T1ID | T1Value |
+------+---------+
|    1 | First   |
|    2 | Second  |
|    3 | Third   |
|    4 | Fourth  |
|    5 | Fifth   |
|    6 | Sixth   |
|    7 | Seventh |
|    8 | Eighth  |
+------+---------+

mysql> use sakila;
Database changed
mysql> show tables;
+----------------------------+
| Tables_in_sakila           |
+----------------------------+
| actor                      |
| actor_info                 |
| address                    |
| category                   |
| city                       |
| country                    |
| customer                   |
| customer_list              |
| film                       |
| film_actor                 |
| film_category              |
| film_list                  |
| film_text                  |
| inventory                  |
| language                   |
| nicer_but_slower_film_list |
| payment                    |
| rental                     |
| sales_by_film_category     |
| sales_by_store             |
| staff                      |
| staff_list                 |
| store                      |
+----------------------------+
23 rows in set (0.01 sec)

mysql> SELECT DISTINCT cust.customer_id, cust.first_name, cust.last_name
    -> FROM customer cust
    -> INNER JOIN rental ren ON ren.customer_id = cust.customer_id
    -> INNER JOIN inventory inv ON inv.inventory_id = ren.inventory_id
    -> INNER JOIN film fl ON fl.film_id = inv.film_id
    -> INNER JOIN film_category fc ON fc.film_id = fl.film_id
    -> INNER JOIN category cat ON cat.category_id = fc.category_id
    -> WHERE cat.name = 'Action'
    -> ORDER BY cust.customer_id, cust.first_name, cust.last_name;
+-------------+-------------+--------------+
| customer_id | first_name  | last_name    |
+-------------+-------------+--------------+
|           1 | MARY        | SMITH        |
|           2 | PATRICIA    | JOHNSON      |
|           3 | LINDA       | WILLIAMS     |
|           4 | BARBARA     | JONES        |
|           5 | ELIZABETH   | BROWN        |
|           6 | JENNIFER    | DAVIS        |
|           7 | MARIA       | MILLER       |
|           8 | SUSAN       | WILSON       |
|          10 | DOROTHY     | TAYLOR       |
|          11 | LISA        | ANDERSON     |

                    . . .
                    
|         583 | MARSHALL    | THORN        |
|         584 | SALVADOR    | TEEL         |
|         585 | PERRY       | SWAFFORD     |
|         587 | SERGIO      | STANFIELD    |
|         588 | MARION      | OCAMPO       |
|         589 | TRACY       | HERRMANN     |
|         590 | SETH        | HANNON       |
|         592 | TERRANCE    | ROUSH        |
|         593 | RENE        | MCALISTER    |
|         594 | EDUARDO     | HIATT        |
|         595 | TERRENCE    | GUNDERSON    |
|         596 | ENRIQUE     | FORSYTHE     |
|         598 | WADE        | DELVALLE     |
|         599 | AUSTIN      | CINTRON      |
+-------------+-------------+--------------+
510 rows in set (0.07 sec)

