# 🧩 Experiment 2: DDL Commands

## 🎯 AIM  
To study and implement **DDL (Data Definition Language)** commands and different types of **constraints** in SQL.

---

## 📘 THEORY  

### **1. CREATE**  
Used to create a new relation (table).  

**Syntax:**
```sql
CREATE TABLE table_name (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```

---

### **2. ALTER**  
Used to add, modify, drop, or rename fields in an existing relation.  

**(a) ADD**
```sql
ALTER TABLE std ADD (Address CHAR(10));
```

**(b) MODIFY**
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```

**(c) DROP**
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```

**(d) RENAME**
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```

---

### **3. DROP TABLE**  
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```

---

### **4. RENAME**  
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```

---

## ⚙️ CONSTRAINTS  

Constraints are rules applied to columns to maintain the integrity, accuracy, and reliability of data.  
They can be added at the time of **table creation** or later using **ALTER TABLE**.

---

### **1. NOT NULL**
Ensures that a column cannot have a NULL value.
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```

---

### **2. UNIQUE**
Ensures all values in a column are unique.
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```

---

### **3. CHECK**
Specifies a condition that each row must satisfy.
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```

---

### **4. PRIMARY KEY**
Uniquely identifies each record in a table.  
- Must contain unique values  
- Cannot be NULL  

```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```

---

### **5. FOREIGN KEY**
Establishes a relationship between two tables.
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```

---

### **6. DEFAULT**
Provides a default value if no value is specified.
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type DEFAULT 'default_value'
);
```

---

## 💻 QUESTIONS & SQL IMPLEMENTATION

### **Question 1**
Add a new column named `discount` with data type `DECIMAL(5,2)` to the **customer** table.

```sql
ALTER TABLE customer
ADD discount DECIMAL(5,2);
```

**Output:**  
![Output 1](https://github.com/user-attachments/assets/b4ef318d-d3d0-46e8-bfca-e89581540fc7)

---

### **Question 2**
Create a table named **Orders** with:
- `OrderID` as **PRIMARY KEY**  
- `OrderDate` as **NOT NULL**  
- `CustomerID` as **FOREIGN KEY** referencing `Customers(CustomerID)`

```sql
CREATE TABLE Orders(
  OrderID INTEGER PRIMARY KEY,
  OrderDate DATE NOT NULL,
  CustomerID INTEGER,
  FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);
```

**Output:**  
![Output 2](https://github.com/user-attachments/assets/4225b99c-b2dc-4ed3-aab8-8259b3fed42c)

---

### **Question 3**
Create a table **contacts** with:
- `contact_id` as PRIMARY KEY  
- `first_name` and `last_name` as NOT NULL  
- `email` as TEXT  
- `phone` with a CHECK constraint (length ≥ 10)

```sql
CREATE TABLE contacts(
  contact_id INTEGER PRIMARY KEY,
  first_name TEXT NOT NULL,
  last_name TEXT NOT NULL,
  email TEXT,
  phone TEXT NOT NULL CHECK(length(phone) >= 10)
);
```

**Output:**  
![Output 3](https://github.com/user-attachments/assets/7ccadc52-75e8-4cc7-9d68-72a13a668539)

---

### **Question 4**
Insert records into `student_details` with different combinations of NULL and filled fields.

```sql
INSERT INTO student_details(RollNo, Name, Gender, Subject, MARKS) VALUES (205, 'Olivia Green', 'F', NULL, NULL);
INSERT INTO student_details(RollNo, Name, Gender, Subject, MARKS) VALUES (207, 'Liam Smith', 'M', 'Mathematic', 85);
INSERT INTO student_details(RollNo, Name, Gender, Subject, MARKS) VALUES (208, 'Sophia Johns', 'F', 'Science', NULL);
```

**Output:**  
![Output 4](https://github.com/user-attachments/assets/eec93418-7c9a-4c0c-bd16-ecfbde374d96)

---

### **Question 5**
Create table **Invoices** with multiple constraints.

```sql
CREATE TABLE Invoices(
  InvoiceID INTEGER PRIMARY KEY,
  InvoiceDate DATE,
  Amount REAL CHECK (Amount > 0),
  DueDate DATE CHECK (DueDate > InvoiceDate),
  OrderID INTEGER,
  FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);
```

**Output:**  
![Output 5](https://github.com/user-attachments/assets/0caad142-d2ba-4e10-ad70-0c0505a4def0)

---

### **Question 6**
Create table **products** with multiple constraints and defaults.

```sql
CREATE TABLE products(
  product_id INTEGER PRIMARY KEY,
  product_name TEXT NOT NULL,
  list_price DECIMAL(10,2) NOT NULL,
  discount DECIMAL(10,2) NOT NULL DEFAULT 0,
  CHECK(list_price >= discount AND discount >= 0 AND list_price >= 0)
);
```

**Output:**  
![Output 6](https://github.com/user-attachments/assets/24cb774a-9f2f-41e0-b525-7f8703ffee80)

---

### **Question 7**
Add two new columns `first_name` and `last_name` to the **employee** table.

```sql
ALTER TABLE employee ADD first_name VARCHAR(50);
ALTER TABLE employee ADD last_name VARCHAR(50);
```

**Output:**  
![Output 7](https://github.com/user-attachments/assets/03c95486-9058-4156-ace5-aafbc39e3556)

---

### **Question 8**
Create a table named **Departments**.

```sql
CREATE TABLE Departments (
  DepartmentID INTEGER,
  DepartmentName TEXT
);
```

**Output:**  
![Output 8](https://github.com/user-attachments/assets/5bfe18ce-6f85-45ac-bffb-6a35d6d1ffcb)

---

### **Question 9**
Insert all records from **Discontinued_products** into **Products**.

```sql
INSERT INTO Products(ProductID, ProductName, Price, Stock)
SELECT ProductID, ProductName, Price, Stock FROM Discontinued_products;
```

**Output:**  
![Output 9](https://github.com/user-attachments/assets/707177aa-1f28-4a8d-9562-0266930972fe)

---

### **Question 10**
Insert a new record into the **Employee** table.

```sql
INSERT INTO Employee(EmployeeID, Name, Position, Department, Salary)
VALUES (001, 'Sarah Parker', 'Manager', 'HR', 60000);
```

**Output:**  
![Output 10]<img width="1501" height="198" alt="image" src="https://github.com/user-attachments/assets/dee164fb-2820-4c96-891b-72b49a95cb9c" />


---

## ✅ RESULT  
Thus, the SQL queries to implement different types of **constraints** and **DDL commands** were executed successfully.
