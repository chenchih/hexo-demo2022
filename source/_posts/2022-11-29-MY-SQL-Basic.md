---
title: MY-SQL(Basic)
date: 2022-11-29 10:52:35
tags: mysql
---

我想分享一些基本的DB(MYSQL)語法。之前面試有考不管是在Amazon，或Microsoft 都有考過我DB。我那時有準備筆記，但後來就不知跑哪。今天想在這篇寫關於SQL基本指令，有機會再寫高階的語法。

我住前是用MYSQL的DB軟體，你們可以選用其他的如MogoDB, Microsoft SQL server，orlacle DB等等。基本上語法都差不多，我猜的

- Table: employee:
```
+----+-------+--------+--------------+
| id | Name  | Salary | DepartmentID |
+----+-------+--------+--------------+
|  1 | Joe   | 85000  | 1            |
|  2 | Henry | 80000  | 2            |
|  3 | Sam   | 60000  | 1            |
|  4 | Max   | 90000  | 1            |
|  5 | Janet | 69000  | 1            |
|  6 | Randy | 85000  | 1            |
+----+-------+--------+--------------+
```

## SELECT & FROM 
### select * from
select 可以選擇要印那一欄，如果加`*`可以把所有內如印出來，以下是指令:
> `select * from employee;`

```
Table: employee;
+----+-------+--------+--------------+
| id | Name  | Salary | DepartmentID |
+----+-------+--------+--------------+
|  1 | Joe   | 85000  | 1            |
|  2 | Henry | 80000  | 2            |
|  3 | Sam   | 60000  | 1            |
|  4 | Max   | 90000  | 1            |
|  5 | Janet | 69000  | 1            |
|  6 | Randy | 85000  | 1            |
+----+-------+--------+--------------+
```

### select Name 指定欄位
> `SELECT Name, Salary From Employee;`

> output:
```
+-------+--------+
| Name  | Salary |
+-------+--------+
| Joe   | 85000  |
| Henry | 80000  |
| Sam   | 60000  |
| Max   | 90000  |
| Janet | 69000  |
| Randy | 85000  |
+-------+--------+
```
### DISTINCT
> `SELECT DISTINCT DepartmentID From Employee;`

```
+--------------+
| DepartmentID |
+--------------+
| 1            |
| 2            |
+--------------+
```

## WHERE
### Where & And 
```
SELECT * From Employee
where DepartmentID =2 AND Salary > 50000;
```

> output:
```
+----+-------+--------+--------------+
| id | Name  | Salary | DepartmentID |
+----+-------+--------+--------------+
|  2 | Henry | 80000  | 2            |
+----+-------+--------+--------------+
```





### Where & or 
```
SELECT * From Employee
where Salary < 70000 OR Salary >80000;
```

> output:
```
+----+-------+--------+--------------+
| id | Name  | Salary | DepartmentID |
+----+-------+--------+--------------+
|  1 | Joe   | 85000  | 1            |
|  3 | Sam   | 60000  | 1            |
|  4 | Max   | 90000  | 1            |
|  5 | Janet | 69000  | 1            |
|  6 | Randy | 85000  | 1            |
+----+-------+--------+--------------+
```

### Where & IN
```
SELECT * From Employee
where Salary < 70000 and Salary < 85000;
```
> output
```
+----+-------+--------+--------------+
| id | Name  | Salary | DepartmentID |
+----+-------+--------+--------------+
|  3 | Sam   | 60000  | 1            |
|  5 | Janet | 69000  | 1            |
+----+-------+--------+--------------+
```
也可以這樣用
```
SELECT * From Employee
where Salary IN (70000 , 85000);
```

> output
```
+----+-------+--------+--------------+
| id | Name  | Salary | DepartmentID |
+----+-------+--------+--------------+
|  1 | Joe   | 85000  | 1            |
|  6 | Randy | 85000  | 1            |
+----+-------+--------+--------------+
```

### Where & like
```
SELECT * From Employee
where Name Like "%an%;
```
> output
```
+----+-------+--------+--------------+
| id | Name  | Salary | DepartmentID |
+----+-------+--------+--------------+
|  5 | Janet | 69000  | 1            |
|  6 | Randy | 85000  | 1            |
+----+-------+--------+--------------+
```

## GROUP BY

### Group BY
```
SELECT DepartmentID, Count(Name)
from Employee Group By DepartmentID;
```
> output
```
+--------------+-------------+
| DepartmentID | Count(Name) |
+--------------+-------------+
| 1            |           5 |
| 2            |           1 |
+--------------+-------------+
```

### Group BY & alias 另取新名
```
SELECT DepartmentID, Count(Name) As Number_Employee
from Employee
Group By DepartmentID;
```
> output
```
+--------------+-------------+
| DepartmentID | Count(Name) |
+--------------+-------------+
| 1            |           5 |
| 2            |           1 |
+--------------+-------------+
```

### Group BY & Aggression function

```
SELECT DepartmentID, Count(Salary) As Total,
Min(Salary) AS MinSalary,
Max(Salary) As MaxSalary,
Avg(Salary) as AvgSalary,
Sum(Salary) as SumSalary
from Employee
Group By DepartmentID;
```

> output
```
+--------------+-------+-----------+-----------+-----------+-----------+
| DepartmentID | Total | MinSalary | MaxSalary | AvgSalary | SumSalary |
+--------------+-------+-----------+-----------+-----------+-----------+
| 1            |     5 | 60000     | 90000     |     77800 |    389000 |
| 2            |     1 | 80000     | 80000     |     80000 |     80000 |
+--------------+-------+-----------+-----------+-----------+-----------+
```

## HAVING & ORDER BY
### Having
```
SELECT DepartmentID
from Employee
Group By DepartmentID
HAVING COUNT(*) > 3;
```
> output:
```
+--------------+
| DepartmentID |
+--------------+
| 1            |
+--------------+
```

### ORDER BY ASC

```
SELECT Name,Salary,DepartmentID
from Employee
order by salary;
```

> output:
```
+-------+--------+--------------+
| Name  | Salary | DepartmentID |
+-------+--------+--------------+
| Sam   | 60000  | 1            |
| Janet | 69000  | 1            |
| Henry | 80000  | 2            |
| Joe   | 85000  | 1            |
| Randy | 85000  | 1            |
| Max   | 90000  | 1            |
+-------+--------+--------------+
```

### ORDER BY ASC Multiply column
```
SELECT Name,Salary,DepartmentID
from Employee
order by salary, DepartmentID;

```

> output

```
+-------+--------+--------------+
| Name  | Salary | DepartmentID |
+-------+--------+--------------+
| Sam   | 60000  | 1            |
| Janet | 69000  | 1            |
| Henry | 80000  | 2            |
| Joe   | 85000  | 1            |
| Randy | 85000  | 1            |
| Max   | 90000  | 1            |
+-------+--------+--------------+
```

### ORDER BY Desc
```
SELECT Name,Salary,DepartmentID
from Employee
order by salary DESC;
```

> output
```
+-------+--------+--------------+
| Name  | Salary | DepartmentID |
+-------+--------+--------------+
| Max   | 90000  | 1            |
| Joe   | 85000  | 1            |
| Randy | 85000  | 1            |
| Henry | 80000  | 2            |
| Janet | 69000  | 1            |
| Sam   | 60000  | 1            |
+-------+--------+--------------+
```

## Join
- Table: employee:
```
+----+-------+--------+--------------+
| id | Name  | Salary | DepartmentID |
+----+-------+--------+--------------+
|  1 | Joe   | 85000  | 1            |
|  2 | Henry | 80000  | 2            |
|  3 | Sam   | 60000  | 1            |
|  4 | Max   | 90000  | 1            |
|  5 | Janet | 69000  | 1            |
|  6 | Randy | 85000  | 1            |
+----+-------+--------+--------------+
```

- Table: department:
```
+----+------+
| ID | name |
+----+------+
|  1 | IT   |
+----+------+
```

### Inner Join
INNER JOIN: returns rows when there is a match in both tables.
```
SELECT Employee.Id as ID,Employee.Name as Name,
Employee.salary as Salary, Employee.DepartmentID as DepartmentID,
Department.Name as DepartmentName
From Employee
INNER JOIN Department
on Employee.DepartmentId=Department.Id;

```
> output:
```
+----+-------+--------+--------------+----------------+
| ID | Name  | Salary | DepartmentID | DepartmentName |
+----+-------+--------+--------------+----------------+
|  1 | Joe   | 85000  | 1            | IT             |
|  3 | Sam   | 60000  | 1            | IT             |
|  4 | Max   | 90000  | 1            | IT             |
|  5 | Janet | 69000  | 1            | IT             |
|  6 | Randy | 85000  | 1            | IT             |
+----+-------+--------+--------------+----------------+
```

### Left Join
LEFT JOIN: returns all rows from the left table, even if there are no matches in the right table.

```
SELECT Employee.Id as ID,Employee.Name as Name,
Employee.salary as Salary, Employee.DepartmentID as DepartmentID,
Department.Name as DepartmentName
From Employee
LEFT JOIN Department
on Employee.DepartmentId=Department.Id;
```

> output:
```
+----+-------+--------+--------------+----------------+
| ID | Name  | Salary | DepartmentID | DepartmentName |
+----+-------+--------+--------------+----------------+
|  1 | Joe   | 85000  | 1            | IT             |
|  2 | Henry | 80000  | 2            | NULL           |
|  3 | Sam   | 60000  | 1            | IT             |
|  4 | Max   | 90000  | 1            | IT             |
|  5 | Janet | 69000  | 1            | IT             |
|  6 | Randy | 85000  | 1            | IT             |
+----+-------+--------+--------------+----------------+
```

### Right Join
RIGHT JOIN: returns all rows from the right table, even if there are no matches in the left table.

```
SELECT Employee.Id as ID,Employee.Name as Name,
Employee.salary as Salary, Employee.DepartmentID as DepartmentID,
Department.Name as DepartmentName
From Employee
RIGHT JOIN Department
on Employee.DepartmentId=Department.Id;

```

> output:

```
+------+-------+--------+--------------+----------------+
| ID   | Name  | Salary | DepartmentID | DepartmentName |
+------+-------+--------+--------------+----------------+
|    1 | Joe   | 85000  | 1            | IT             |
|    3 | Sam   | 60000  | 1            | IT             |
|    4 | Max   | 90000  | 1            | IT             |
|    5 | Janet | 69000  | 1            | IT             |
|    6 | Randy | 85000  | 1            | IT             |
+------+-------+--------+--------------+----------------+
```