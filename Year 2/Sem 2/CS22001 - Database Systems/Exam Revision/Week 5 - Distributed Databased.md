# What is a Distributed Database?
As data size and processing requirements grow, databases often must be spread across multiple sites. A distributed database is defined as  "a logically inter-related collection of shared data (and  description of this data), which is physically distributed over a computer network." In other words, while the data is stored in different locations, the distributed DBMS (or DDBMS) makes it appear to users as if it is one single, unified database. This transparency is key for simplifying user access despite the underlying complexity.

# Core Concepts of Distributed Databases
## Distribution and Fragmentation
### Fragmentation
The data within a distributed database is split into smaller parts, known as fragments. There are different ways to fragment data:
- **Horizontal Fragmentation**: In which the table is split by records (rows)
- **Vertical Fragmentation**: Where the table is divided by attributes (columns)
- **Hybrid Fragmentation**: A mix of both horizontal and vertical approaches
Breaking the data into fragments allows each piece to be managed more effectively and placed on appropriate nodes within the network
## Replication
- Fragments may be replicated (copied) and stored at more than once site
- Replication increases availability and can improve query performance because data can be retrieved from the nearest or least busy node
## Allocation Strategies
The distribution of fragments and replicas across sites can follow different strategies
- **Centralised**: The entire database is stored at one site even though users access it over the network
- **Partitioned**: The database is partitioned into disjoint fragments, with each fragment assigned to a specific site
- **Complete Replication**: Each site maintains a full copy of the database 
- **Selective Replication**: A hybrid approach combining partitioning, replication, and centralisation
Each strategy has its own advantages and trade-offs - for example, while replication offers redundancy and availability, it also increases complexity in ensuring consistency between copies.
# Requirements for a Distributed DBMS
To support distributed data, a DDBMS must offer everythinhg that a traditional DBMS provides, with additional features including:
- **Extended communication services**: These are needed for inter-site communication
- **Distributed query processing**: For handling queries that span multiple sites transparently
- **Extended concurrency**: To ensure that transactions across different sites do not interfere with each other
- **Extended recovery services**: Because failures can occur at one site, the DDBMS must coordinate recovery so that the global database remains consistent

# Parallel DBMS vs. Distributed DBMS
There is a difference between parallel and distributed DBMSs:
- **Parallel DBMSs** run across multiple processors or disks within the same site to improve throughput and reliability
- **Distributed DBMSs** manage databases that are geographically distributed with sites that are separately administered
The two approaches both aim to enhance performance but address different challenges. In a distributed system, issues such as network latency and independent administration must be managed.
# Distributed Transaction Management
Transactions in a distributed environment bring extra complexity because they may span several sites:
- A **distributed transaction** is a sequence of operations that reads or updates data on two or more distinct nodes
- Each global transaction is divided into **sub-transactions**, one for each site involved
- The key requirement is that the entire transaction remains atomic - either every sub-transaction commits or they all roll back. Synchronizing these sub-transactions is critical for maintaining the database's integrity across different locations
# Transparency in Distributed DBMSs
Transparency is a recurring theme. The DDBMS hides the underlying distributed complexity by providing several types of transparencies:
- **Distribution Transparency**: Users interact with the data as if it were stored in one location without needing to specify fragment names or locations
- **Fragmentation Transparency**: Users need not know that the data is split into fragments
- **Replication Transparency**: The system hides the fact that certain data is replicated across multiple sites
- **Transaction Transparency**: Despite a global transaction being split into sub-transactions, the commit or rollback appears as a single, indivisible operation
- **Concurrency and Failure Transparency**: The system manages concurrent access across sites and recovers from failures without exposing these problems to users
The goal is to present the complexity of distributed data storage and processing as a simple unified database service
