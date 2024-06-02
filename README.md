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
