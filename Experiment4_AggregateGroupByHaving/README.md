# Experiment 4: Aggregate Functions, Group By and Having Clause
## Name: ASTLE JOE A S
## Reg.no:212224240019
## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**

How many prescriptions were written by each doctor?

Sample tablePrescriptions Table
```
SELECT DoctorID, COUNT(*)AS
TotalPrescriptions
FROM Prescriptions
GROUP BY DoctorID;
```
**Output:**

![image](https://github.com/user-attachments/assets/c5ecb054-0dcb-4489-baa4-2b30c8238a73)

**Question 2**

How many patients are covered by each insurance company?

Sample table:Insurance Table

name type

InsuranceID INTEGER PatientID INTEGER InsuranceCompany TEXT PolicyNumber TEXT PolicyHolder TEXT ValidityPeriod TEXT

```
SELECT InsuranceCompany,
COUNT ( DISTINCT PatientID )AS
TotalPatients
FROM Insurance
GROUP BY InsuranceCompany;
```
**Output:**

![image](https://github.com/user-attachments/assets/02784127-99c3-429f-ad06-d69b605a5c7b)

**Question 3**

How many patients are there in each city?

```
SELECT Address, COUNT(*)AS
TotalPatients
FROM Patients
GROUP BY Address;
```
**Output:**

![image](https://github.com/user-attachments/assets/38f989b2-c1f9-4278-8f02-1497e0eebb7a)


**Question 4**

Write a SQL query to find the minimum purchase amount.

Sample table: orders

ord_no purch_amt ord_date customer_id salesman_id

70001 150.5 2012-10-05 3005 5002

70009 270.65 2012-09-10 3001 5005

70002 65.26 2012-10-05 3002 5001

```
SELECT MIN(purch_amt)AS
MINIMUM
FROM orders;
```
**Output:**

![image](https://github.com/user-attachments/assets/77336749-974a-44be-ba09-0ec0fd4e04ad)


**Question 5**

Write a SQL query to return the total number of rows in the 'customer' table where the city is not Noida.
```
SELECT COUNT(*)AS 
COUNT
FROM customer
WHERE city!='Noida';
```
**Output:**

![image](https://github.com/user-attachments/assets/d1974d6a-e83a-47df-aa64-0256aea51d3e)


**Question 6**

Write a SQL query to find the maximum purchase amount.

Sample table: orders

ord_no purch_amt ord_date customer_id salesman_id

70001 150.5 2012-10-05 3005 5002

70009 270.65 2012-09-10 3001 5005

70002 65.26 2012-10-05 3002 5001

```
SELECT MAX (purch_amt)AS MAXIMUM
FROM orders;
```
**Output:**

![image](https://github.com/user-attachments/assets/f6e9c531-1bcb-4bb9-bbaa-a6c0b8485a12)


**Question 7**

Write a SQL query to Calculate the average email length (in characters) for people who lives in Mumbai city

Table: customer

name type

id INTEGER name TEXT
city TEXT email TEXT phone INTEGER

```
SELECT AVG(LENGTH(email))AS
avg_email_length_below_30
FROM customer
WHERE city='Mumbai';
```
**Output:**

![image](https://github.com/user-attachments/assets/ca601445-a16b-442f-aae8-0900b5334b75)


**Question 8**

Write the SQL query that achieves the grouping of data by age intervals using the expression (age/5)5, calculates the average age for each group, and excludes groups where the average age is not less than 24.
```
SELECT
  (age/5)*5 AS age_group ,
   AVG(age)
FROM customer1
GROUP BY age_group 
HAVING AVG(age)<24;
```
**Output:**

![image](https://github.com/user-attachments/assets/3b0e0130-41c2-42cb-b857-2688573e0f7e)


**Question 9**

Write the SQL query that achieves the selection of category and calculates the sum of the product of price and category ID as Revenue for each category from the "products" table, and includes only those products where the total revenue is greater than 25.
```
SELECT CATEGORY_ID, SUM(price*category_id) AS Revenue
FROM products
GROUP BY category_id
HAVING SUM(price *category_id)>25;
```
**Output:**

![image](https://github.com/user-attachments/assets/dcd2a606-3aaf-466c-ba73-ae9acfbc394b)


**Question 10**

How many medical records are there for each patient?
```
select PatientID, count(RecordID) as 'TotalRecords'
from MedicalRecords
group by PatientID;
```
**Output:**

![image](https://github.com/user-attachments/assets/b45b235a-cc86-420d-84ac-4c4a3aefb6d5)

## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
