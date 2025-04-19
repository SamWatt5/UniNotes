Written Questions:

1.

According to Bill Inmon's definition, what are the four key characteristics of a data warehouse?1

2.


Explain the difference between OLTP systems and data warehouses, focusing on their purpose and the nature of their data.2

3.

Describe the OLAP operations of roll-up and drill-down, and provide an example of each.3

4.

What is the primary goal of data mining, and what distinguishes it from a random search?4

5.

Name and briefly describe three key data mining operations and their goals.5 ...

6.

What does the acronym CRUDS stand for in the context of database operations?7

7.

Explain the key difference between SQL being procedural versus non-procedural.8

8.

List and briefly describe three clauses commonly used in advanced SQL SELECT statements.9

9.

What are the four ACID properties of a database transaction, and why are they important?10

10.

Explain the purpose of database locking in the context of transaction concurrency and name the two main types of locks.11

11.

What are the three core security objectives for a database?12

12.

Define a distributed database and explain the key concept of transparency associated with it.13 ...

13.

Differentiate between horizontal and vertical fragmentation in a distributed database.15

14.

Explain the core trade-offs presented by the CAP Theorem in the context of distributed databases.16 ...

15.

Contrast the ACID properties of traditional databases with the BASE principles often associated with NoSQL databases.17

16.

Describe the document data model used in MongoDB, including the terms database, collections, and documents.18

17.

What are the primary benefits of using replication in a database system like MongoDB?18 ...

18.

Explain how a shard key is used in MongoDB for horizontal scaling (sharding).20

19.

In graph databases, what do nodes and edges represent, and why are graph databases well-suited for analyzing relationships?21 ...

20.

Describe the difference in data modeling between relational databases and graph databases when representing relationships.23

Multiple Choice Questions:

21.

Which of the following is NOT a key characteristic of a data warehouse according to the provided source? a) Subject-oriented1 b) Transactional2 c) Time-variant24 d) Non-volatile24

22.

Data warehouses primarily support: a) Online Transaction Processing (OLTP)2 b) Recording day-to-day transactions2 c) Decision support through Business Intelligence25 ... d) Overwriting older data2

23.

Aggregating quarterly sales data into annual totals is an example of which OLAP operation? a) Drill-down3 b) Slice27 c) Roll-up3 d) Pivot27

24.

Identifying groups of similar customers for targeted marketing campaigns is an application of which data mining operation? a) Predictive Modelling5 b) Database Segmentation5 c) Link Analysis6 d) Deviation Detection6

25.

Finding "if-then" relationships between products in a market basket analysis is an example of: a) Classification5 b) Value prediction5 c) Association discovery6 d) Sequential pattern discovery6

26.

Which SQL command is used to retrieve existing records from a database? a) INSERT INTO8 b) UPDATE8 c) DELETE8 d) SELECT8

27.

The SQL clause used to add conditions to filter the rows in a query is: a) FROM9 b) WHERE9 c) GROUP BY9 d) ORDER BY9

28.

Which ACID property ensures that all operations within a transaction are completed successfully or none are? a) Consistency10 b) Isolation10 c) Durability10 d) Atomicity10

29.

A situation where two transactions are each waiting for resources held by the other is known as: a) Lost Update11 b) Uncommitted Dependency11 c) Deadlock11 d) Dirty Read10

30.

Preventing unauthorized updates to data addresses which core database security objective? a) Confidentiality12 b) Integrity12 c) Availability12 d) Authentication28

31.

Splitting a database table by records (rows) into smaller parts in a distributed database is called: a) Replication29 b) Vertical Fragmentation15 c) Horizontal Fragmentation15 d) Allocation29

32.

Ensuring that a transaction across multiple sites either fully commits or fully rolls back demonstrates: a) Distribution Transparency14 b) Replication Transparency14 c) Transaction Transparency14 d) Fragmentation Transparency14

33.

In the context of the CAP Theorem, a system that prioritizes all clients receiving a response, even if some data might be inconsistent, is known as a(n): a) CP system17 b) ACID system17 c) AP system17 d) BASE system17

34.

Which type of NoSQL database stores data as key-value pairs? a) Document Databases30 b) Graph Databases31 c) Key-Value Databases32 d) Column-Family Databases33

35.

Storing an author's contact information directly within the author's document in MongoDB is an example of: a) Referencing34 b) Embedding35 c) Linking21 d) Joining36

36.

In MongoDB replication, which node handles all write operations by default? a) Secondary Node19 b) Arbiter Node19 c) Primary Node19 d) Shard Router20

37.

What is the critical field used to determine the distribution of documents across shards in MongoDB? a) Index Key37 b) Replication Key19 c) Shard Key20 d) Primary Key18

38.

Which MongoDB aggregation pipeline stage filters documents based on specified criteria? a) $group38 b) $sort38 c) $project38 d) $match38 ...

39.

In a graph database representing a social network, the relationship between two users being "friends" would be represented by: a) A node21 b) An edge21 c) An attribute21 d) A property21

40.

Which type of database is particularly optimized for queries that involve traversing relationships between data points? a) Relational Databases40 b) Document Databases30 c) Key-Value Databases32 d) Graph Databases22

keep_pinSave to note

copy_all

thumb_up

thumb_down