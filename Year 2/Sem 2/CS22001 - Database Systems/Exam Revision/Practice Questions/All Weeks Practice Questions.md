
## Written Questions

### 1. Describe the role of primary keys and foreign keys in relational database design and how they support relationships between tables.
Primary keys are attributes of a table that uniquely identify each record. Foreign keys are attributes of a table that contain the primary key of another table. This is used to create relationships
[[All Weeks Answers#^e5dec8|Answer]]
### 2. Explain what a functional dependency is in the context of relational databases and why it matters for normalization.
a functional is dependency is where 
[[All Weeks Answers#^8f99a6|Answer]]
### 3. Compare and contrast the first, second, and third normal forms (1NF, 2NF, 3NF), detailing the types of anomalies each form is designed to eliminate.
1NF is used to eliminate insertion anomalies. It does this first by making attributes only contain a single value. It also 
2NF is used to eliminate deletion anomalies. It does this by making sure attributes are only dependent on the primary key.
3NF is used to eliminate 
[[All Weeks Answers#^6dd0d5|Answer]]
### 4. Draw (or describe) an Entity–Relationship diagram for a library system with the entities Book, Author, and Loan, including cardinalities and key attributes.
![[Pasted image 20250417135422.png]]
[[All Weeks Answers#^c6012e|Answer]]
### 5. Write an SQL SELECT query to retrieve the names and addresses of all customers who rented a property in the first quarter of 2025, ordering the results by rental date.
```SQL
SELECT (c.name, c.address)
FROM Customers AS c
JOIN Rentals AS r
ON c.customerID = r.customerID
WHERE r.rentalDate < DATE("01-04-2025")
ORDER BY r.rentalDate;
```
[[All Weeks Answers#^65138c|Answer]]
### 6. Given two tables, Orders(order_id, customer_id, order_date) and Customers(customer_id, name), write an SQL query to find the names of customers who have never placed an order.
```SQL
SELECT name
FROM Customers
WHERE customer_id NOT IN (SELECT customer_id FROM Orders);
```
[[All Weeks Answers#^b4a4f0|Answer]]
### 7. Explain the purpose of SQL views, and provide an example scenario in which a view enhances security.
SQL views are used to restrict which users can see certain contents in a database. An example of this could be if a table contains sensitive user information, such as their phone number, which should only be seen by users with admin privileges. A view can be created to make sure regular users cannot see the phone number attribute.
[[All Weeks Answers#^f75bc5|Answer]]
### 8. Outline the four ACID properties of database transactions and give a real‑world example illustrating each one.
**A**: Atomicity
This means that either transactions happen in full, or, if there is a single failure, nothing changes
**C**: Consistency
This means that all users see the same thing at all times
**I**: Isolation
This means that no changes are visible to other users until the transaction is committed
**D**: Durability
This means that, in the event of a crash, committed changes still persist
[[All Weeks Answers#^da4057|Answer]]
### 9. Discuss common issues with transaction concurrency (e.g., lost updates) and explain how share (read) and exclusive (write) locks help prevent these anomalies.

[[All Weeks Answers#^6f1dbd|Answer]]
### 10. Describe how SQL injection attacks work and name two techniques for mitigating them.
SQL injections work by entering an SQL statement into an input field. If, for example, there was a login page, with a username field, the page may inject the entry from the username field directly into an SQL statement, i.e. SELECT * FROM Users WHERE username = {{ENTRY}}; if the user ends the SQL query early, using a semicolon, they can enter their own query. This can be used to access database entries without permission. SQL injections can be mitigated by cleansing entries before putting them into a query (i.e. if they start with a semicolon, remove it), or by not allowing certain characters (i.e. semicolons)
[[All Weeks Answers#^f412bc|Answer]]
### 11. In a distributed database system, explain the difference between fragmentation and replication strategies, and give an example of each.
fragmentation is where you split up a database, so that different locations contain different information, e.g. split by region. Replication is where the same data is replicated across different servers. 
[[All Weeks Answers#^073933|Answer]]
### 12. List and explain three types of transparency that a distributed DBMS provides to hide the complexity of distribution from end users.
replication transparency - users see a single database
location transparency - users are unaware of database location
fragmentation transparency - users are unaware of fragmentation
[[All Weeks Answers#^f289f4|Answer]]
### 13. Compare homogeneous and heterogeneous distributed database environments, and discuss one major challenge unique to heterogeneous systems.

[[All Weeks Answers#^87bcc2|Answer]]
### 14. State the CAP theorem and explain the trade‑offs a system must make between consistency, availability, and partition tolerance.
CAP stands for Consistency, Availability and Partition tolerance.

### 15. Distinguish between the ACID and BASE transaction models in NoSQL systems.
ACID is 
BASE is

### 16. Compare the four major NoSQL database types—key‑value, document, column‑family, and graph—by giving a characteristic use case for each.
key-values are used for quick lookups, i.e. for a game leaderboard
document is great for 
column family is
graph databases are best for showing relationships between nodes, i.e. for a social network, showing who is friends with who etc.

### 17. Explain the difference between embedding and referencing in MongoDB schema design, and state one advantage and one disadvantage of each approach.
Embedding is where information that could be a whole item is embedded inside of an attribute of another schema, whereas referencing is where a schema holds a reference to an item in another schema, for example holding the id of an item. Embedding is useful for information that is only accessed at the same time, and referencing is great for information that is accessed separately, as if one thing is updated, it doesn't need to update the information in multiple places.

### 18. Describe MongoDB’s sharding and replication mechanisms (including the role of shard keys and replica sets) and discuss when to create indexes, noting any performance trade‑offs.

### 19. For a graph database, outline in pseudocode how you would find the shortest path between two nodes, and explain why graph databases are particularly efficient for multi‑hop queries.

### 20. Define data warehousing and data mining, and describe one benefit and one challenge associated with implementing a data warehouse.
Data warehousing is storing historical data for analysis. Data mining is the act of analysing the data in a data warehouse. One challenge associated with implementing a data warehouse is 

## Multiple Choice Questions

### 1. Which of the following is TRUE about a composite primary key?

a. It must consist of exactly two attributes.  
b. It can uniquely identify a record using multiple attributes.  
c. It cannot be used to establish foreign key relationships.  
d. It always requires a surrogate key to be added.

B
### 2. Which SQL clause is used to sort the result set?

a. WHERE  
b. ORDER BY  
c. GROUP BY  
d. HAVING

B
### 3. The aggregate function that counts the number of non-null values in a column is:

a. SUM  
b. COUNT  
c. AVG  
d. MAX

B
### 4. An INNER JOIN between tables A and B returns:

a. All rows from A.  
b. All rows from B.  
c. Rows with matching keys in both A and B.  
d. Rows in A that have no match in B.

C
### 5. A database view is best described as:

a. A physical copy of a table.  
b. A virtual table defined by a query.  
c. An index on a set of columns.  
d. A stored procedure.

B
### 6. Which SQL statement makes all changes in the current transaction permanent?

a. ROLLBACK  
b. COMMIT  
c. SAVEPOINT  
d. BEGIN TRANSACTION

B
### 7. The “lost update” problem in concurrent transactions is most directly prevented by using:

a. Read locks.  
b. Write locks.  
c. Saving intermediate results.  
d. Disabling autocommit.

B
### 8. Which of these is a best practice to prevent SQL injection?

a. Concatenating user inputs into SQL strings.  
b. Using parameterised queries.  
c. Granting broad permissions to all users.  
d. Relying on client‑side validation only.

B
### 9. In distributed databases, what does “complete replication” mean?

a. A single central copy is maintained.  
b. Each fragment is stored at exactly one site.  
c. Every site holds a full copy of the database.  
d. Only hot data is replicated.

C
### 10. Which transparency lets users query a distributed database without knowing where fragments reside?

a. Fragmentation transparency  
b. Location transparency  
c. Replication transparency  
d. Transaction transparency

B
### 11. In a homogeneous DDBMS:

a. Sites run different DBMS software.  
b. All sites run the same DBMS software.  
c. No replication is permitted.  
d. Queries must use ODBC for access.

B
### 12. According to the CAP theorem, during a network partition you must choose between:

a. Consistency and Partition tolerance  
b. Availability and Partition tolerance  
c. Consistency and Availability  
d. Security and Performance


### 13. Which NoSQL model stores data as JSON‑like documents?

a. Key‑Value  
b. Document  
c. Column‑Family  
d. Graph

B
### 14. In MongoDB schema design, embedding is preferred when:

a. The embedded data changes frequently.  
b. The embedded array can grow without bound.  
c. Related data is always accessed together.  
d. You need strict normalization.

C
### 15. A good shard key should exhibit:

a. Low cardinality.  
b. Monotonically increasing values.  
c. Even distribution across a large keyspace.  
d. Values identical for most documents.

C
### 16. In a MongoDB replica set, which node handles all write operations by default?

a. Secondary  
b. Arbiter  
c. Primary  
d. Config server


### 17. In a property graph database, nodes represent {blank} and edges represent {blank}.

a. Relationships; entities  
b. Tables; rows  
c. Entities; relationships  
d. Columns; tables

C
### 18. Which OLAP operation aggregates data to a higher level?

a. Drill‑down  
b. Slice  
c. Roll‑up  
d. Pivot

C
### 19. In data mining, the process of grouping similar records without predefined labels is called:

a. Classification  
b. Regression  
c. Clustering  
d. Prediction

C
### 20. Deviation detection in data mining is primarily used to identify:

a. Future trends  
b. Outliers  
c. Frequent item sets  
d. Decision boundaries

B