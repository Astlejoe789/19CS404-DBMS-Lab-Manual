# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
-- Write a SQL query to Add a new column named "discount" with the data type DECIMAL(5,2) to the "customer" table.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
 

For example:

Test	Result
pragma table_info('customer');
cid         name         type                               notnull     dflt_value  pk
----------  -----------  ---------------------------------  ----------  ----------  ----------
0           customer_id  integer primarykey auto increment  0                       0
1           cust_name    varchar2(30)                       0                       0
2           city         varchar(30)                        0                       0
3           grade        number                             0                       0
4           salesman_id  number                             0                       0
5           discount     DECIMAL(5,2)                       0                       0

```sql
-- ALTER table customer
add  discount DECIMAL(5,2)
```

**Output:**

<img width="1867" height="289" alt="image" src="https://github.com/user-attachments/assets/b4ef318d-d3d0-46e8-bfca-e89581540fc7" />


**Question 2**
---
-- Create a table named Orders with the following constraints:
OrderID as INTEGER should be the primary key.
OrderDate as DATE should be not NULL.
CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).
For example:

Test	Result
INSERT INTO Customers (CustomerID, FirstName, LastName, Email) VALUES (1, 'Alice', 'Johnson', 'alice.johnson@example.com');
INSERT INTO Orders (OrderID, OrderDate, CustomerID) VALUES (1, '2024-08-01', 1);
select * from orders;
OrderID     OrderDate   CustomerID
----------  ----------  ----------
1           2024-08-01  1


```sql
-- create table Orders(
OrderID INTEGER primary key,
OrderDate DATE not null,
CustomerID INTEGER,
FOREIGN KEY (CustomerID) references Customers(CustomerID)
);
```

**Output:**

<img width="1893" height="342" alt="image" src="https://github.com/user-attachments/assets/4225b99c-b2dc-4ed3-aab8-8259b3fed42c" />


**Question 3**
---
-- Create a new table named contacts with the following specifications:
contact_id as INTEGER and primary key.
first_name as TEXT and not NULL.
last_name as TEXT and not NULL.
email as TEXT.
phone as TEXT and not NULL with a check constraint to ensure the length of phone is at least 10 characters.


```sql
-- create table contacts(
contact_id INTEGER PRIMARY KEY,
first_name TEXT NOT NULL,
last_name TEXT NOT NULL,
email TEXT,
phone TEXT NOT NULL CHECK(length(phone)>=10)
);
```

**Output:**

<img width="1898" height="229" alt="image" src="https://github.com/user-attachments/assets/7ccadc52-75e8-4cc7-9d68-72a13a668539" />


**Question 4**
---
-- In the Student_details table, insert a student record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

RollNo      Name            Gender      Subject      MARKS
----------  ------------    ----------  ----------   ----------
205         Olivia Green    F
207         Liam Smith      M           Mathematics  85
208         Sophia Johnson  F           Science

```sql
-- INSERT INTO student_details(RollNo,Name,Gender, Subject,MARKS) VALUES (205, 'Olivia Green', 'F',NULL,NULL);

INSERT INTO student_details(RollNo,Name,Gender, Subject,MARKS) VALUES (207, 'Liam Smith', 'M','Mathematic',85);

INSERT INTO student_details(RollNo,Name,Gender, Subject,MARKS) VALUES (208, 'Sophia Johns', 'F','Science',NULL)
```

**Output:**

<img width="1741" height="303" alt="image" src="https://github.com/user-attachments/assets/eec93418-7c9a-4c0c-bd16-ecfbde374d96" />


**Question 5**
---
-- Create a table named Invoices with the following constraints:
InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
Amount as REAL should be greater than 0.
DueDate as DATE should be greater than the InvoiceDate.
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).


```sql
-- create table Invoices(
InvoiceID INTEGER PRIMARY KEY,
InvoiceDate DATE,
Amount REAL CHECK (Amount>0),
DueDate DATE CHECK (DueDate>InvoiceDate),
OrderID INTEGER ,
FOREIGN KEY (OrderID) references Orders(OrderID)
);
```

**Output:**

<img width="1867" height="209" alt="image" src="https://github.com/user-attachments/assets/0caad142-d2ba-4e10-ad70-0c0505a4def0" />


**Question 6**
---
-- Create a new table named products with the following specifications:
product_id as INTEGER and primary key.
product_name as TEXT and not NULL.
list_price as DECIMAL (10, 2) and not NULL.
discount as DECIMAL (10, 2) with a default value of 0 and not NULL.
A CHECK constraint at the table level to ensure:
list_price is greater than or equal to discount
discount is greater than or equal to 0
list_price is greater than or equal to 0


```sql
-- create table products(
product_id INTEGER PRIMARY KEY,
product_name TEXT NOT NULL,
list_price DECIMAL(10,2) NOT NULL, 
discount DECIMAL(10,2) NOT NULL DEFAULT 0,
CHECK(list_price>=discount AND discount>=0 AND list_price>=0)
);
```

**Output:**

<img width="1853" height="236" alt="image" src="https://github.com/user-attachments/assets/24cb774a-9f2f-41e0-b525-7f8703ffee80" />


**Question 7**
---
--  Write an SQL query to add two new columns, first_name and last_name, to the table employee. Both columns should have a data type of varchar(50).

```sql
-- ALTER TABLE employee
add first_name varchar(50);
alter table employee
add last_name varchar(50);
```

**Output:**

<img width="1840" height="317" alt="image" src="https://github.com/user-attachments/assets/03c95486-9058-4156-ace5-aafbc39e3556" />


**Question 8**
---
-- Create a table named Departments with the following columns:

DepartmentID as INTEGER
DepartmentName as TEXT

```sql
-- create table Departments (
DepartmentID INTEGER,
DepartmentName TEXT
);
```

**Output:**

<img width="1450" height="276" alt="image" src="https://github.com/user-attachments/assets/5bfe18ce-6f85-45ac-bffb-6a35d6d1ffcb" />


**Question 9**
---
-- Insert all products from Discontinued_products into Products.

Table attributes are ProductID, ProductName, Price, Stock

```sql
-- INSERT into Products( ProductID, ProductName, Price, Stock)
select  ProductID, ProductName, Price, Stock from Discontinued_products;
```

**Output:**

<img width="1501" height="198" alt="image" src="https://github.com/user-attachments/assets/707177aa-1f28-4a8d-9562-0266930972fe" />


**Question 10**
---
-- Insert a record with EmployeeID 001, Name Sarah Parker, Position Manager, Department HR, and Salary 60000 into the Employee table.

```sql
-- insert into Employee(EmployeeID , Name ,Position ,Department  ,Salary) values(001,'Sarah Parker','Manager','HR',60000);
```

**Output:**

![Uploading image.png…]()



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
