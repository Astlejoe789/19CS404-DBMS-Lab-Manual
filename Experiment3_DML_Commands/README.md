# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
-- What is the most common time slot for appointments for each doctor?

```sql
-- SELECT DoctorID, TimeSlot, COUNT(*) AS TotalAppointments
FROM Appointments
GROUP BY DoctorID, TimeSlot
HAVING COUNT(*) = (
    SELECT MAX(COUNT(*))
    FROM Appointments AS A2
    WHERE A2.DoctorID = Appointments.DoctorID
    GROUP BY A2.TimeSlot
);
```

**Output:**

<img width="379" height="233" alt="image" src="https://github.com/user-attachments/assets/356851f9-59ed-4355-a375-c34995a141b1" />


**Question 2**
---
-- How many patients are there in each city?

```sql
-- SELECT Address, COUNT(*) AS TotalPatients
FROM Patients
GROUP BY Address;

```

**Output:**

<img width="1197" height="405" alt="image" src="https://github.com/user-attachments/assets/e5b9f486-f6f8-4860-8735-217e1fcd50ac" />


**Question 3**
---
-- How many patients are covered by each insurance company?

```sql
-- SELECT InsuranceCompany, COUNT(DISTINCT PatientID) AS TotalPatients
FROM Insurance
GROUP BY InsuranceCompany;
```

**Output:**

<img width="820" height="658" alt="image" src="https://github.com/user-attachments/assets/7b965e43-0957-4405-a194-6091672d7a32" />


**Question 4**
---
-- Write a SQL query to find the total amount of fruits with a unit type of 'LB'.

```sql
-- SELECT SUM(inventory) AS total
FROM fruits
WHERE unit = 'LB';
```

**Output:**

<img width="574" height="306" alt="image" src="https://github.com/user-attachments/assets/f4f6ec6f-587c-4de2-b711-46ac57bb8ae7" />


**Question 5**
---
-- Paste Question 5 here

```sql
-- Paste your SQL code below for Question 5
```

**Output:**

![Output5](output.png)

**Question 6**
---
-- Write a SQL query to calculate the average purchase amount of all orders. Return average purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

```sql
-- SELECT AVG(purch_amt) AS AVERAGE
FROM orders;
```

**Output:**

-<img width="665" height="299" alt="image" src="https://github.com/user-attachments/assets/e22f0134-404a-42c0-aa0d-ed0900699263" />


**Question 7**
---
-- Write a SQL query to find the minimum purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

```sql
-- Paste your SQL code below for Question 7
```

**Output:**

![Output7](output.png)

**Question 8**
---
-- Paste Question 8 here

```sql
-- SELECT MIN(purch_amt) AS MINIMUM
FROM orders;
```

**Output:**

<img width="477" height="304" alt="image" src="https://github.com/user-attachments/assets/c08eac1f-84f9-4e6b-9294-98b228c271ea" />


**Question 9**
---
-- Write the SQL query that accomplishes the selection of product which has lowest price in each category from the "products" table and includes only those products where the minimum price is less than 10.

```sql
-- SELECT category_id, MIN(price) AS Price
FROM products
GROUP BY category_id
HAVING MIN(price) < 10;
```

**Output:**

<img width="776" height="508" alt="image" src="https://github.com/user-attachments/assets/b530b6ef-7bb8-452e-94d2-0d8effaa62ca" />


**Question 10**
---
-- Write the SQL query that accomplishes the selection of total number of products for each category from the "products" table, and includes only those products where the minimum category ID is less than 3.

```sql
-- SELECT category_id, count(product_name)
FROM products
WHERE category_id < 3
GROUP BY category_id;
```

**Output:**

<img width="759" height="358" alt="image" src="https://github.com/user-attachments/assets/fd902d57-d3ff-40b4-b68c-decb862d8adb" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
