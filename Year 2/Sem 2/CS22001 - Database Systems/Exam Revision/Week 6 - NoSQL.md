# Context and Motivation
## The Limitations of Traditional Databases
Traditional databases are designed for high consistency, data integrity, and use established query standards. They are build with predefined schemas, which can limit flexibility and sometimes struggle when scaling (especially with unstructured or rapidly growing data).
## Big Data Attributes
The term "Big Data" extends beyond sheer volume. It encapsulated the following factors:
- **Volume**: Handling large quantities of data
- **Velocity**: Dealing with data arriving at a high speed
- **Variety**: Integrating information from many sources
- **Value**: Extracting actionable wisdom from data
- **Veracity**: Determining which data is real and reliable
# Scaling: Vertical vs. Horizontal
## Vertical Scaling
Involves upgrading a single server with more CPU and memory. It is simpler but has inherent limits
## Horizontal Scaling
Involves adding more machines to distribute the load, offering near-infinite scalability. However it introduces complexity in coordinating data across many nodes
# The CAP Theorem
## Components of CAP
- **Consistency**: Every client sees the same data at the same time, no matter which node they access
- **Availability**: Every client receives a response, even if one or more nodes are down
- **Partition Tolerance**: The system continues to operate despite network partitions or failures
## Trade-offs in Practice
The CAP theorem shows that in the event of a network partition, a distributed database can only guarantee either consistency or availability. Different systems (CP or AP databases) are designed based on which of these qualities they prioritize
## ACID vs. BASE
- **ACID** (Atomicity, Consistency, Isolation, Durability) characterizes traditional transactional databases
- **BASE** (basically Available, Soft-state, Eventually consistent) is used to describe many NoSQL systems. These systems relax immediate consistency guarantees to gain scalability and flexibility.
# What are NoSQL Databases?
## "Not Only SQL"
NoSQL databases provide schema-less data models and much flexibility compared to relational databases. Instead of storing data in tables, NoSQL systems may store data in various formats:
- **Key-Value pairs**
- **JSON-based documents**
- **Graphs (node-edge models)**
- **Column families**
# Flavours of NoSQL Databases
## Flavour 1: Key-Value Databases
### Overview
They represent data as a simple key and a value pair. A hash function typically maps keys to store and retrieve values
### Use Cases
Ideal for session management, caching, and real-time updates (e.g. game leaderboard and quick look-ups)
### Advantages
Super-simple structure, very flexible, and extremely fast
### Disadvantages
Too simple for relationships, no built-in support for joins, and you can only search by key
## Flavour 2: Document Databases
### Overview
These databases store data in a semi-structured format (for example, JSON or XML). Entire documents are stored as records, making it possible to have a flexible schema where fields can vary between records
### Advantages:
Flexibility in data structure, nested data support, and the ability to search by value
## Flavour 3: Graph Databases
### Overview
They use an explicit graph structure with nodes (vertices) and relationships (edges) to store data. This model is highly effective for scenarios where relationships (such as social networks or recommendation systems) are a priority.
### Advantages
Fast for multi-hop queries and relationships; the distance (in steps) between connected nodes remains small even as the dataset grows.
## Flavour 4: Column-Family Databases
### Overview
These provide a flexible schema where each row can have different columns. Related columns are stored together, making them suitable for applications like content management systems and handling time-series data.
### Advantages
Good for dynamic data models where columns may be added without modifying the database structure.
## Query-Driven Design
One of the key shifts with NoSQL is the focus on how you will access data rather than how you store it. With SQL databases, the design question is "How do i store this data?" In contrast, NoSQL drives you to ask, "How will i access this data?"