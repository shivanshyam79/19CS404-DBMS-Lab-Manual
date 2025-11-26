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
<img width="1204" height="394" alt="image" src="https://github.com/user-attachments/assets/7b76ade5-efcb-4ac4-8b35-a96c88f49b87" />


```
CREATE TABLE Attendance (
    AttendanceID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    AttendanceDate DATE,
    Status TEXT CHECK (Status IN ('Present', 'Absent', 'Leave')),
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
);
```

**Output:**

<img width="1227" height="314" alt="image" src="https://github.com/user-attachments/assets/a796f049-da73-4fe6-a080-47c4b2ce8c2e" />


**Question 2**

---
<img width="1116" height="476" alt="image" src="https://github.com/user-attachments/assets/388602c5-fae6-4796-b414-f365815f5d60" />


```
CREATE TABLE Attendance (
    AttendanceID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    AttendanceDate DATE,
    Status TEXT CHECK (Status IN ('Present', 'Absent', 'Leave')),
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
);
```

**Output:**

<img width="1230" height="434" alt="image" src="https://github.com/user-attachments/assets/2a18d710-8e6f-42c8-b294-10f888ff9d14" />


**Question 3**

<img width="1116" height="476" alt="image" src="https://github.com/user-attachments/assets/f09806b9-069a-430c-b57a-06bcc86b860e" />



```
CREATE TABLE Item (
    item_id TEXT PRIMARY KEY,
    item_desc TEXT NOT NULL,
    rate INTEGER NOT NULL,
    icom_id TEXT CHECK (LENGTH(icom_id) = 4),
    FOREIGN KEY (icom_id) REFERENCES Company(com_id)
        ON UPDATE CASCADE
        ON DELETE CASCADE
);
```

**Output:**

<img width="1229" height="339" alt="image" src="https://github.com/user-attachments/assets/bce955c0-0f39-4288-93a5-d662435c7369" />


**Question 4**

<img width="1216" height="375" alt="image" src="https://github.com/user-attachments/assets/6234affd-cdb8-4958-82c2-1cdda35c5cc5" />

```
ALTER TABLE employee
ADD first_name varchar(50);

ALTER TABLE employee
ADD last_name varchar(50);
```

**Output:**

<img width="1212" height="398" alt="image" src="https://github.com/user-attachments/assets/7e065d7e-f2b3-4c58-ad9a-5abe38a3cfe7" />


**Question 5**
---
<img width="1237" height="508" alt="image" src="https://github.com/user-attachments/assets/028be329-f1a8-4cb2-8df9-73a17bae0f16" />


```sql
INSERT INTO Products (ProductID, Name, Category)
VALUES (106, 'Fitness Tracker', 'Wearables');

INSERT INTO Products (ProductID, Name, Category, Price, Stock)
VALUES (107, 'Laptop', 'Electronics', 999.99, 50);

INSERT INTO Products (ProductID, Name, Category, Stock)
VALUES (108, 'Wireless Earbuds', 'Accessories', 100);
```

**Output:**

<img width="1233" height="376" alt="image" src="https://github.com/user-attachments/assets/f635a3ae-1358-4fd6-900d-50c331b55017" />


**Question 6**
---
<img width="1225" height="418" alt="image" src="https://github.com/user-attachments/assets/3fcf8f13-5be4-4d1b-9c76-367439fd5ad7" />


```
CREATE TABLE Employees (
    EmployeeID INTEGER PRIMARY KEY,
    FirstName TEXT NOT NULL,
    LastName TEXT NOT NULL,
    Email TEXT UNIQUE,
    Salary REAL CHECK (Salary > 0),
    DepartmentID INTEGER,
    FOREIGN KEY (DepartmentID) REFERENCES Departments(DepartmentID)
);
```

**Output:**

<img width="1227" height="498" alt="image" src="https://github.com/user-attachments/assets/e02518c2-5528-4e70-b395-63fc2a40bfc7" />



**Question 7**
---
<img width="1202" height="356" alt="image" src="https://github.com/user-attachments/assets/ceaef433-4f28-4466-8242-1f375fc5bcaa" />


```
CREATE TABLE Department (
    DepartmentID INTEGER PRIMARY KEY,
    DepartmentName TEXT NOT NULL UNIQUE,
    Location TEXT
);
```

**Output:**

<img width="1227" height="353" alt="image" src="https://github.com/user-attachments/assets/f2edcfb9-d9e1-4bc3-ad0c-34e56c57ccc5" />


**Question 8**
---
<img width="1135" height="398" alt="image" src="https://github.com/user-attachments/assets/4657f5cd-c8ff-4b56-a925-9a9e0fc51811" />


```
CREATE TABLE Tasks (
    TaskID INTEGER,
    TaskName TEXT,
    DueDate DATE
);
```

**Output:**

<img width="1229" height="467" alt="image" src="https://github.com/user-attachments/assets/cce1cbd2-b812-4e64-b622-e36cf91b8df5" />


**Question 9**
---
<img width="1196" height="297" alt="image" src="https://github.com/user-attachments/assets/2343b27a-66ab-411e-a422-016b3ee3cd40" />


```
INSERT INTO Books (ISBN, Title, Author, Publisher, Year)
VALUES ('978-1234567890', 'Data Science Essentials', 'Jane Doe', 'TechBooks', 2024);
```

**Output:**

<img width="1234" height="331" alt="image" src="https://github.com/user-attachments/assets/67287cbf-09f9-4950-b6fe-568e1032741d" />


**Question 10**
---
<img width="1155" height="583" alt="image" src="https://github.com/user-attachments/assets/3ff42331-fe20-4cb1-a634-dd7aab3f2ca8" />


```
ALTER TABLE Student_details
ADD Mobilenumber number;
```

**Output:**

<img width="1229" height="453" alt="image" src="https://github.com/user-attachments/assets/6f9e024d-8622-4472-808d-cbdffd9187d4" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
