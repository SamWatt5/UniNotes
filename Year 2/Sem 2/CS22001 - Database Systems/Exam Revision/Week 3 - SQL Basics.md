## CRUDS Operations
The essential database operations are summarized by the acronym **CRUDS**:
- **Create**: Adding new records (or tables)
- **Read**: Retrieving existing records
- **Update**: Modifying records
- **Delete**: Removing records
- **Search**: Finding specific records without modification

## What is SQL
### Definition and History
**SQL** (Structured Query Language) is a command-line scription language designed for interacting with relational databases. It originated in the 70s with IBM's development of the relational model. Despite its textual nature, SQL is designed to be highly readable and relatively easy to learn
### Key Features
- SQL is non-procedural, so you state what information is required, rather than how to retrieve it
- It is case-insensitive and supports a free-format style of writing commands

## Basic SQL Commands and Operations
### Fundamental Commands
- `CREATE TABLE`: To define new tables (usually performed only once)
- `INSERT INTO`: To add new records
- `UPDATE`: To change existing records
- `DELETE`: To remove records
### Simple Examples
#### Insertion
```SQL
INSERT INTO Students (Name, Address, Phone)
VALUES ("Sam", "94 Nethergate", "07443526226");
```
#### Update
```SQL
UPDATE Students
SET Address = "41 Polton Bank", Phone = "07740945751"
WHERE Name = "Sam";
```
#### Deletion
```SQL
DELETE FROM Students
WHERE Name = "Sam";
```

## The SELECT Statement and Querying
### Basic SELECT Statement
- The **SELECT** statement is used for reading or searching records. For example, to retrieve all columns from a table you use:
	`SELECT * FROM Students;`
- To retrieve specific columns, list them (e.g., `SELECT StudentNo, FName, LName, Course FROM Students;`)
### Ordering Output
- An example of an advanced SELECT is sorting the results:
	`SELECT StaffNo, FName, LName, Salary FROM Staff ORDER BY Salary DESC`
### Query Clauses Overview
- **FROM**: Specifies the table(s) to be used
- **WHERE**: Adds conditions to filter the rows.
- **GROUP BY**: Aggregates rows with the same values in specified columns
- **HAVING**: Filters groups created by **GROUP BY** based on aggregate conditions
- **ORDER BY**: Sorts the final result set

## Aggregate Functions and Grouping
### Aggregate Functions
- **Count**: Returns the number of rows or non-null values
- **Sum**: Returns the total sum of numerical values
- **AVG**: Returns the average of numerical values
- **MIN/MAX** Returns the smallest or largest value, respectively
#### Examples: 
To count properties costing more than a certain rent:
```SQL
SELECT COUNT(*) AS MyCount
FROM PropertyForRent
WHERE Rent > 350;
```
To find the total, minimum, and maximum salaries:
```SQL
SELECT MIN(Salary) AS MyMin, MAX(Salary) AS MyMax, AVG(Salary) AS MyAvg
FROM Staff;
```
### Grouping Records
- Use the **GROUP BY** clause to aggregate data by a specific column. For instance, this will find the total number of staff and their combined salary for each branch:
```SQL
SELECT BranchNo, COUNT(StaffNo) as MyCount, SUM(Salary) AS MySum
FROM Staff
GROUP BY BranchNo
ORDER BY BranchNo;
```
### Filtering Groups
- The **HAVING** clause is used to filter groups. For example, to include only branches with more than one staff member:
```SQL
SELECT BranchNo, COUNT(StaffNo) as MyCount, SUM(Salary) AS MySum
FROM Staff
GROUP BY BranchNo
HAVING COUNT(StaffNo) > 1
ORDER BY BranchNo;
```
## Subqueries and Joins
### Subqueries
- A Subquery (or nested query) is a **SELECT** statement embedded inside another SQL statement. It is often used in **WHERE** or **HAVING** clauses to further filter the results
- Example: To list staff working at a branch located at '163 Main St':
```SQL
SELECT staffNo fName, lName, position 
FROM Staff 
WHERE branchNo = (
	SELECT branchNo
	FROM Branch
	WHERE street = "163 Main ST"
);
```
### Joins Across Multiple Tables
- When data from more than one table is required in the result, you need to join the tables. 
- A common join is the **inner join**, where rows from two tables match based on a condition
- Example using explicit join syntax:
```SQL
SELECT C.clientNo, fName, lName, propertyNo, comment
FROM Client C
JOIN Viewing V ON C.clientNo = V.clientNo;
```
- The slides also mention variants like LEFT, RIGHT, and FULL OUTER JOINs
