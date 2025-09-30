# Week 2 - Database Design
## E-R Modelling (entities, attributes, relationships)
- Entities are the tables of the database
- Attributes are the columns (name, age, userID, etc.)
- relationships are how an entity connects to another entity (e.g. an Author WRITES books)

## Normalisation (1NF, 2NF, 3NF)
### 1NF
- all rows are single data type
- all items are single-value (no lists)
- no duplicate rows or columns

### 2NF
- in 1NF
- all attributes are reliant on the whole primary key
### 3NF
- in 2NF
- remove transitive dependencies (non-key attributes depending on non-key attributes)
## Functional Dependencies

## Relationship types and key selection
### types of relationships
1..\*, 0..\*, 0..1, 1..1 etc.
### types of keys
#### candidate key
an attribute or attributes of a table that can uniquely identify each row - possible choice for primary key
#### primary key
the attribute of a table that uniquely identifies each row
#### foreign key
the primary key of another table, used for linking multiple tables
#### composite key
a primary key that is split across multiple attributes

# Week 3 - SQL Basics
## SELECT query syntax and statement ordering
SELECT - information to show
FROM - which table to use
JOINS - for foreign key linking
WHERE - conditional
GROUP BY - groups information
HAVING - like WHERE but for groups
ORDER BY - self explanatory (can do DESC)
;

## Aggregates (SUM, COUNT, MAX, MIN, AVG)


## Using JOINs properly and their different types
### INNER JOIN
only shows information that is in both tables
### LEFT JOIN
only shows information that is in the left table (the one being selected on)
### RIGHT JOIN
only shows information that is in the right table (the one being joined with)
### FULL JOIN
shows all information from both tables
# Week 4 - Views, transactions and security
## Views - what are they and why are they used?
### What are views
views are virtual tables, that reveal specified information. 
### Why are they used
To restrict access to certain information for security reasons, or to show only relevant information
## Properties of ACID transactions
### What is a transaction?
A transaction is a sql query that will either complete completely, or, if there are any failures in the completion process, will roll back to before the transaction started
### A - Atomicity
All or nothing - Either the transaction completes in full, or not at all
### C - Consistency
Must leave the database in a valid state
### I - Isolation
Transactions cant interfere with one another. Transactions don't show any intermediary stages
### D - Durability
As soon as a transaction completes, its changes are permanent. 
## Issues with transaction concurrency
### Issues
#### lost data
This is where two transactions update the same record, and one overwrites the other
#### Uncommitted dependency
This is where one transaction reads data that another is currently writing
#### Deadlock
this is where two transactions wait for each other's resources, causing a standstill
### Solutions
Locking is used to make sure issues don't occur. Shared (read) locks are used to make sure that multiple transactions can read the same date simultaneously. Exclusive (write) locks are used to make sure that when a transaction is updating data, no other transaction can read or write that same data until the lock is released.
## Security issues (including SQL injection)
Security is critical in database systems. 
### Core security objectives
**Confidentiality**: Data must only be accessed by the intended users. Personal data and financial figures must be hidden.
**Integrity**: Data must not be able to be tampered with (updated or deleted)
**Availability**: Data must always be accessible, even in the event of hardware failures or attacks

### Threats and Countermeasures
Data can be compromised by methods like SQL injection, where an unauthorized user injects malicious queries into the database.
#### Countermeasures
Threats can be reduced with the following methods:
- **Access Controls**: SQL `GRANT` and `REVOKE` statements can be use to give/remove permissions from a user
- **Encryption**: If encrypted data is intercepted, it still cannot be read
- **Backup and recovery**: if data is changed, a backup can be used to restore the data to its previous state
- **Safeguards against SQL injection**: Parameterized statements and sanitizing inputs can be used to prevent SQL injections
# Week 5 - Distributed Databases
## Advantages + Disadvantages
### Advantages
- In the case of a network failure, data is still accessible
- Queries are made more efficient
- Data can be held where it is most relevant
- Scalability

### Disadvantages
- Higher cost
- Security challenges
- Integrity is harder to maintain

## Replication strategies
### Centralised
Database stored in one location, with users distributed across the network
### Partitioned
Data is split across different locations
### Complete Replication
all data is duplicated at each location
### Selective Replication
combination of all of the above
## Homogeneous vs. Heterogeneous
### Homogeneous
Homogeneous is where all nodes of a DDBMS use the same DBMS, i.e. all mySQL, all MongoDB, all Oracle etc...
- Improved performance
- Easier to manage
### Heterogeneous
Heterogeneous is where not all nodes use the same DBMS, i.e. some use mySQL, some use mongoDB, some use postgreSQL.
- This is typically because of legacy systems
- Translations are typically required
## Types of transparency
### Distribution Transparency
Users interact with the data as if it were stored in one location
### Fragmentation Transparency
Users don't need to know that the data is split across multiple locations
### Replication Transparency
The system hides the fact that there are duplicated across the network
### Transaction Transparency
Despite transactions being split into sub-transactions for each node, they act as one transactions. If one fails, they all fail
### Concurrency Transparency
The system manages concurrent access across sites
### Failure Transparency
The system recovers from failures without exposing them to the user
# Week 6 - NoSQL
## CAP Theorem
CAP theorem states that a distributed database can only have two of the following:
#### C: Consistency
Data is always up-to-date, from whichever node is accessed.
#### A: Availability
Every client always receives a response, even if a part of the network is down
#### P: Partition Tolerance
The system always works, even in the case of network partitions or failures

Realistically, Partition tolerance always needs to be achieved, so there must be a choice between consistency and availability. In a CP system, the data returned is always up-to-date, but if a network failure occurs, there will be no response. In an AP system, data is always returned, even in the case of network partitions, but it may not be up-to-date

## ACID vs BASE transaction models
ACID (Atomicity, Consistency, Isolation, Durability) is used for traditional databases.
BASE (Basically Available, Soft-state, Eventually Consistent) is often used for noSQL databases, this is because it trades off the immediate consistency from ACID for greater scalability and flexibility.


## Different NoSQL database types (Key-Value, Document, Column Family)
### Key-Value
Key value
### Document

### Column Family
Column family databases 
# Week 7 - MongoDB
## Sharding and Replication

## Basic MongoDB query types

## When and when not to use indexes

# Week 8 - Graph Databases
## Properties of Graph Databases

## Understanding what they're good for

## Understanding what they're not good for

## Basic pseudocode for graph queries

# Week 9 - Data Modelling in MongoDB
## The benefits and drawbacks of embedding vs. referencing

## Embedding should be used unless there's a good reason not to

## Data items that frequently change should be referenced

## Avoid lookups where possible

## Avoid lookups where possible

# Week 10 - Data Warehousing and Mining
## The benefits of Data Warehousing

## The challenges of Data Warehousing

## Types of Data Warehousing operations (rollup, slice, dice, etc)

## Types of Data Mining (predictive modelling, database segmentation, etc)