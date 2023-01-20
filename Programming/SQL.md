# SQL

- Structured Query Language
- Although SQL is an ANSI/ISO standard, there are different versions of the SQL language. However, to be compliant with the ANSI standard, they all support at least the major commands (such as ` SELECT`, `UPDATE`, ` DELETE`, `INSERT`, ` WHERE`) in a similar manner.
- RDBMS is the basis for SQL, and for all modern database systems such as  MS SQL Server, IBM DB2, Oracle, MySQL, and Microsoft Access.
- The data in RDBMS is stored in database objects called tables. A table  is a collection of related data entries and it consists of columns and  rows.

### SQL Statements

```sql
SELECT * FROM Customers;
```

- SQL keywords are NOT case sensitive: **select** is the same as **SELECT**

- Semicolon is the standard way to separate each SQL statement in database  systems that allow more than one SQL statement to be executed in the same call  to the server

### Important SQL Commands

| Commands        | Function                         |
| --------------- | -------------------------------- |
| SELECT          | extracts data from a database    |
| UPDATE          | updates data in a database       |
| DELETE          | deletes data from a database     |
| INSERT INTO     | inserts new data into a database |
| CREATE DATABASE | creates a new database           |
| ALTER DATABASE  | modifies a database              |
| CREATE TABLE    | creates a new table              |
| ALTER TABLE     | modifies a table                 |
| DROP TABLE      | deletes a table                  |
| CREATE INDEX    | creates an index (search key)    |
| DROP INDEX      | deletes an index                 |

#### Creating a Table

```sql
CREATE TABLE products(
	id INT NOT NULL,
	name STRING,
	price MONEY,
	PRIMARY KEY (id)
)
```

#### SELECT Statement

```SQL
SELECT column1, column2, ...
FROM table_name;
```

#### SELECT DISTINCT statement

```SQL
/* return only distinct (different) values */
SELECT DISTINCT column1, column2, ...
FROM tablename; 

/* lists the number of different (distinct) items */
SELECT COUNT(DISTINCT column1) FROM tablename;
```

#### SQL WHERE CLAUSE

```SQL
SELECT column1, column2, ...
FROM table_name
WHERE condition; 

SELECT * FROM Customers
WHERE Country='Mexico'; 
```

- SQL requires single quotes around text values (most database systems will  also allow double quotes).

  However, numeric fields should not be enclosed in quotes

- Operators in the WHERE Clause

  | Operators | Description                                                  |      |
  | --------- | ------------------------------------------------------------ | ---- |
  | >         | Greater than                                                 |      |
  | <         | Less than                                                    |      |
  | >=        | Greater than or equal                                        |      |
  | <=        | Less than or equal                                           |      |
  | <>        | Not equal. **Note:** In some versions of SQL this operator may be written as != |      |
  | BETWEEN   | Between a certain range                                      |      |
  | LIKE      | Search for a pattern                                         |      |
  | IN        | To specify multiple possible values for a column             |      |

  **Note:** The `WHERE` clause is not only used in ` SELECT` statements, it is also used in `UPDATE`, `DELETE`, etc.!

#### The SQL AND, OR, and NOT Operators

```SQL
SELECT column1, column2, ...
FROM table_name
WHERE condition1 AND condition2 AND condition3 ...; 

SELECT column1, column2, ...
FROM table_name
WHERE condition1 OR condition2 OR condition3 ...; 

SELECT column1, column2, ...
FROM table_name
WHERE NOT condition; 

/* Example 1 */
SELECT * FROM Customers
WHERE Country='Germany' AND (City='Berlin' OR City='München'); 

/* Example 2 */
SELECT * FROM Customers
WHERE NOT Country='Germany' AND NOT Country='USA'; 
```

#### SQL ORDER BY Keyword

```SQL
SELECT column1, column2, ...
FROM table_name
ORDER BY column1, column2, ... ASC|DESC; 

/* Example */
SELECT * FROM Customers
ORDER BY Country DESC; 
```

#### SQL INSERT INTO Statement

```SQl
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...); 
```

```SQl
/* If you are adding values for all the columns of the table */
INSERT INTO table_name
VALUES (value1, value2, value3, ...); 

/* Example */
INSERT INTO Customers (CustomerName, ContactName, Address, City, PostalCode, Country)
VALUES ('Cardinal', 'Tom B. Erichsen', 'Skagen 21', 'Stavanger', '4006', 'Norway');

/* Insert Data Only in Specified Columns */
INSERT INTO Customers (CustomerName, City, Country)
VALUES ('Cardinal', 'Stavanger', 'Norway');
```

#### SQL NULL VALUE

```SQL
SELECT column_names
FROM table_name
WHERE column_name IS NULL; 

SELECT CustomerName, ContactName, Address
FROM Customers
WHERE Address IS NULL;
```

- If a field in a table is optional, it is possible to insert a new record or  update a record without adding a value to this field. Then, the field will be  saved with a NULL value

#### SQL UPDATE Statement

```SQL
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition; 

/* Example */
UPDATE Customers
SET ContactName = 'Satish Karki', City= 'Mississauga'
WHERE CustomerID = 1;
```

**Note:** Be careful when updating records in a table! Notice the ` WHERE` clause in the `UPDATE` statement. The `WHERE` clause specifies which record(s) that should be updated. If  you omit the `WHERE` clause, all records in the table will be updated!

#### SQL DELETE Statement

```SQL
DELETE FROM table_name WHERE condition;

/* Example */
DELETE FROM Customers WHERE CustomerName='Satish Karki';
/* Delete All Records */
DELETE FROM table_name;
```

**Note:** Be careful when deleting records in a table! Notice the ` WHERE` clause in the  `DELETE` statement. The `WHERE` clause specifies which record(s) should be deleted. If  you omit the `WHERE` clause, all records in the table will be deleted!

There is a lot more  to know about the SQL. Now that you have your feet wet, you can start with the basic operations in SQL and explore more advanced things.


### References

https://www.w3schools.com/sql/sql_intro.asp