
mysql> CREATE TABLE Departments (
    ->          DepartmentID INT PRIMARY KEY,        -- Unique identifier for each department
    ->         DepartmentName VARCHAR(50) NOT NULL -- Name of the department
    ->      );
Query OK, 0 rows affected (0.01 sec)

mysql> INSERT INTO Departments (DepartmentID, DepartmentName)
    ->        VALUES 
    ->        (101, 'HR'),
    ->        (102, 'IT'),
    ->        (103, 'Finance'),
    ->        (104, 'Marketing');
Query OK, 4 rows affected (0.00 sec)
Records: 4  Duplicates: 0  Warnings: 0

mysql> CREATE TABLE Employees (
    ->        EmployeeID INT PRIMARY KEY,          -- Unique identifier for each employee
    ->        Name VARCHAR(50) NOT NULL,           -- Employee's name
    ->        DepartmentID INT,                    -- Foreign key referencing DepartmentID
    ->        Salary DECIMAL(10, 2),               -- Employee's salary
    ->        FOREIGN KEY (DepartmentID) REFERENCES Departments(DepartmentID)
    ->      );
Query OK, 0 rows affected (0.01 sec)

mysql> INSERT INTO Employees (EmployeeID, Name, DepartmentID, Salary)
    ->      VALUES 
    ->      (1, 'John Doe', 101, 50000.00),
    ->      (2, 'Jane Smith', 102, 60000.00),
    ->      (3, 'Alice Jones', NULL, 70000.00),  -- Employee not assigned to any department
    ->      (4, 'Bob Brown', 103, 55000.00);
Query OK, 4 rows affected (0.00 sec)
Records: 4  Duplicates: 0  Warnings: 0

mysql> select * from Departments;
+--------------+----------------+
| DepartmentID | DepartmentName |
+--------------+----------------+
|          101 | HR             |
|          102 | IT             |
|          103 | Finance        |
|          104 | Marketing      |
+--------------+----------------+
4 rows in set (0.00 sec)

mysql> select * from Employees;
+------------+-------------+--------------+----------+
| EmployeeID | Name        | DepartmentID | Salary   |
+------------+-------------+--------------+----------+
|          1 | John Doe    |          101 | 50000.00 |
|          2 | Jane Smith  |          102 | 60000.00 |
|          3 | Alice Jones |         NULL | 70000.00 |
|          4 | Bob Brown   |          103 | 55000.00 |
+------------+-------------+--------------+----------+
4 rows in set (0.00 sec)

mysql> SELECT 
    ->          Employees.EmployeeID,
    ->          Employees.Name,
    ->          Employees.Salary,
    ->          Departments.DepartmentName
    ->          FROM 
    ->          Employees
    ->          INNER JOIN 
    ->          Departments
    ->          ON 
    ->          Employees.DepartmentID = Departments.DepartmentID;
+------------+------------+----------+----------------+
| EmployeeID | Name       | Salary   | DepartmentName |
+------------+------------+----------+----------------+
|          1 | John Doe   | 50000.00 | HR             |
|          2 | Jane Smith | 60000.00 | IT             |
|          4 | Bob Brown  | 55000.00 | Finance        |
+------------+------------+----------+----------------+
3 rows in set (0.00 sec)

mysql> SELECT 
    ->          Employees.EmployeeID,
    ->          Employees.Name,
    ->          Employees.Salary,
    ->          Departments.DepartmentName
    ->          FROM 
    ->          Employees
    ->          LEFT JOIN 
    ->          Departments
    ->          ON 
    ->          Employees.DepartmentID = Departments.DepartmentID;
+------------+-------------+----------+----------------+
| EmployeeID | Name        | Salary   | DepartmentName |
+------------+-------------+----------+----------------+
|          1 | John Doe    | 50000.00 | HR             |
|          2 | Jane Smith  | 60000.00 | IT             |
|          3 | Alice Jones | 70000.00 | NULL           |
|          4 | Bob Brown   | 55000.00 | Finance        |
+------------+-------------+----------+----------------+
4 rows in set (0.00 sec)

mysql> SELECT 
    ->        Employees.EmployeeID,
    ->        Employees.Name,
    ->        Employees.Salary,
    ->        Departments.DepartmentName
    ->        FROM 
    ->        Employees
    ->        RIGHT JOIN 
    ->        Departments
    ->        ON 
    ->        Employees.DepartmentID = Departments.DepartmentID;
+------------+------------+----------+----------------+
| EmployeeID | Name       | Salary   | DepartmentName |
+------------+------------+----------+----------------+
|          1 | John Doe   | 50000.00 | HR             |
|          2 | Jane Smith | 60000.00 | IT             |
|          4 | Bob Brown  | 55000.00 | Finance        |
|       NULL | NULL       |     NULL | Marketing      |
+------------+------------+----------+----------------+
4 rows in set (0.00 sec)

mysql> SELECT 
    ->        Employees.EmployeeID,
    ->        Employees.Name,
    ->        Employees.Salary,
    ->        Departments.DepartmentName
    ->        FROM 
    ->        Employees
    ->        LEFT JOIN 
    ->        Departments
    ->        ON 
    ->        Employees.DepartmentID = Departments.DepartmentID
    ->    
    ->        UNION
    ->     
    ->        SELECT 
    ->         Employees.EmployeeID,
    ->         Employees.Name,
    ->         Employees.Salary,
    ->         Departments.DepartmentName
    ->         FROM 
    ->         Employees
    ->         RIGHT JOIN 
    ->         Departments
    ->         ON 
    ->         Employees.DepartmentID = Departments.DepartmentID;
+------------+-------------+----------+----------------+
| EmployeeID | Name        | Salary   | DepartmentName |
+------------+-------------+----------+----------------+
|          1 | John Doe    | 50000.00 | HR             |
|          2 | Jane Smith  | 60000.00 | IT             |
|          3 | Alice Jones | 70000.00 | NULL           |
|          4 | Bob Brown   | 55000.00 | Finance        |
|       NULL | NULL        |     NULL | Marketing      |
+------------+-------------+----------+----------------+
5 rows in set (0.00 sec)





