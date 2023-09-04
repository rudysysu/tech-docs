## Order by Field
```
https://dba.stackexchange.com/questions/109120/how-does-order-by-field-in-mysql-work-internally

+----+---------+
| id |  name   |
+----+---------+
|  1 | stan    |
|  2 | kyle    |
|  3 | kenny   |
|  4 | cartman |
+----+---------+ 

SELECT * FROM mytable WHERE id IN (3,2,1,4) ORDER BY FIELD(id,3,2,1,4)
The query above will result in

+----+---------+
| id |  name   |
+----+---------+
|  3 | kenny   |
|  2 | kyle    |
|  1 | stan    |
|  4 | cartman |
+----+---------+ 
something similar to saying ORDER BY 3, 2, 1, 4
```