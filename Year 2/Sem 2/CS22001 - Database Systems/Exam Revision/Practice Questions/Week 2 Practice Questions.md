### 1. Define an Entity‑Relationship (ER) diagram and explain its role in database design.
An E-R diagram is a graphical representation of the tables in a database, and their columns. They also show the relationship between the different tables. 

### 2. Describe the main elements of an ER diagram, including entities, attributes, and relationships.
The main part of an E-R diagram is the entities, this contains the table name, and also contains the names of each attribute. Normally the primary key is denoted, as well as any foreign keys. Relationships between entities are denoted as lines, usually with their relationship written too, as well as any multiplicities.

### 3. What is meant by “conceptual model” in database design? Explain how it relates to the requirements phase.

### 4. Explain the purpose of normalization. Why is normalization important in designing a relational database?
Normalization is used to reduce and remove anomalies. This is important to maintain integrity in the database.

### 5. What is the First Normal Form (1NF) and what are its key requirements?
First normal form means that there must be a primary key in the table. This means that each record is unique. It also states that each attribute must contain only one value, meaning no lists. Also it states that there must be no duplicate rows or columns

### 6. Outline the differences between 2NF and 3NF. What additional anomalies do these normal forms address?
2NF is a form that means that all rows are dependent on the primary key. Without it, if a table exists where there is only one instance of an attribute, and that record gets deleted, it will remove the rest of that record. It reduces deletion anomalies.
Third normal form is used

### 7. Define a candidate key. How does it differ from a primary key?
A candidate key is is an attribute that uniquely identifies the row, that could be chosen as the primary key

### 8. Explain what is meant by a composite key and provide an example scenario where it might be used.
A composite key is a primary key that is split across two attributes. One example of this could be for a videogame, where there is a table of each players inventory items. The composite key could be the player name and the item name, which would uniquely identify the record.

### 9. What is a foreign key and how does it facilitate relationships between tables without duplicating data?
a foreign key is an attribute that references the primary key of another table. This allows queries, which use two tables, since the foreign key is equal to the primary key.

### 10. Describe the concept of a joining (junction) table in the context of many-to-many relationships. Why is it necessary?
The best way to describe a joining table is with an example. Imagine a database that stores artists and songs. Many artists can work together on a song, and an artist can make many songs. If the artists of the songs were stored in the song table, it could cause lists of artists, if there were many artists working on a song, which is bad. Instead, a new table could be created, called something like Artist_Song that contains a unique ID for that relationship, along with a song and artist attribute. This allows a many-to-many relationship to happen.

### 11. Explain partial dependency and how it relates to the move from 1NF to 2NF.
Partial dependen

### 12. Define transitive dependency. How does this affect the design of a relational database?

### 13. What are the typical data anomalies (insertion, update, deletion) that normalization aims to eliminate? Provide an example for one anomaly.

### 14. Discuss what constitutes a “good” primary key. List at least three characteristics.

### 15. How do functional dependencies help in the normalization process? Give an example.

### 16. Explain the concept of total versus partial participation in relationships within an ER diagram.

### 17. When an entity is considered weak, what does that imply about its existence and relationship to other entities?

### 18. Describe the process of mapping an ER diagram to a relational schema. What are the key steps involved?

### 19. How can normalization improve data integrity and reduce redundancy in a relational database?

### 20. Provide a real-world example where improper design (lack of normalization) could lead to significant data anomalies. Explain how normalization would help mitigate these issues.


### 1.
Which of the following best describes a candidate key?  
A. A set of attributes that may or may not uniquely identify a record.  
B. A minimal set of attributes that uniquely identifies each record in a table.  
C. The key chosen by the database designer for indexing purposes.  
D. A composite key that is always comprised of two or more attributes.

B
### 2.
Which normal form first requires that all non-key attributes are fully functionally dependent on the primary key?  
A. 1NF  
B. 2NF  
C. 3NF  
D. BCNF

B
### 3.
In an ER diagram, a weak entity:  
A. Can exist independently of any other entity.  
B. Has a primary key that is derived from a related strong entity.  
C. Does not participate in any relationships.  
D. Must always have a composite primary key.

B
### 4.
A composite key is best described as:  
A. A key that is automatically generated by the database.  
B. A key consisting of a single attribute.  
C. A key composed of two or more attributes that uniquely identifies a record.  
D. A key used only in many-to-many relationships.

C
### 5.
What is the primary role of a foreign key in a relational database?  
A. To ensure that each table has a unique identifier.  
B. To enforce referential integrity by linking two tables together.  
C. To optimize query performance with indexing.  
D. To store redundant data for faster retrieval.

B
### 6.
Total participation in a relationship indicates that:  
A. Some instances of the entity may not be involved in the relationship.  
B. Every instance of the entity must participate in the relationship.  
C. The entity is weak.  
D. The relationship must have a composite key.

B
### 7.
Which normal form specifically addresses the removal of transitive dependencies?  
A. 1NF  
B. 2NF  
C. 3NF  
D. BCNF

C
### 8.
In many-to-many relationships, the table that breaks the relationship into two one-to-many relationships is known as:  
A. A linking table.  
B. A composite table.  
C. A candidate table.  
D. A primary table.

A
### 9.
A good primary key should ideally be:  
A. Multi-valued and non-unique.  
B. Single-attribute, numerical, and stable.  
C. A composite of as many attributes as possible.  
D. Derived from user inputs and frequently updated.

B
### 10.
Normalization primarily serves to:  
A. Increase the physical storage requirements of a database.  
B. Simplify complex SQL queries by denormalizing the data.  
C. Eliminate data redundancy and improve data integrity.  
D. Create additional indexes for faster data retrieval.

C
### 11.
Which of the following anomalies is NOT typically addressed by normalization?  
A. Insertion anomaly.  
B. Update anomaly.  
C. Deletion anomaly.  
D. Reporting anomaly.

D
### 12.
In a relational database, relationships between tables are typically established using:  
A. Primary keys only.  
B. Foreign keys only.  
C. Both primary and foreign keys.  
D. Indexes exclusively.

B
### 13.
The primary purpose of an ER diagram is to:  
A. Provide a visual representation of the database’s logical structure.  
B. Specify the physical storage details of a database.  
C. List every single record in the database.  
D. Automatically generate SQL queries.

A
### 14.
Which key uniquely identifies every record in a table?  
A. Foreign key  
B. Primary key  
C. Candidate key  
D. Composite key

B
### 15.
One of the requirements of First Normal Form (1NF) is that:  
A. Each table must have a composite key.  
B. Each cell in a table must contain only a single value.  
C. There must be no foreign keys.  
D. Data redundancy must be eliminated completely.


### 16.
A foreign key:  
A. Uniquely identifies each record in its own table.  
B. Is used to establish a relationship between two tables.  
C. Must always be a composite key.  
D. Is automatically generated and cannot be defined by the designer.

### 17.
How are many-to-many relationships typically implemented in a relational database?  
A. By merging the two related tables into one.  
B. By creating a separate joining table with foreign keys from each table.  
C. By embedding one table’s attributes into the other.  
D. By using only composite keys in both tables.

### 18.
Partial dependency occurs when:  
A. A non-key attribute depends on the whole primary key.  
B. A non-key attribute depends on only part of a composite primary key.  
C. A key attribute is duplicated across two tables.  
D. A foreign key depends on the candidate key.

### 19.
Transitive dependency is present when:  
A. A non-key attribute depends directly on the primary key.  
B. A non-key attribute depends on another non-key attribute that is itself dependent on the primary key.  
C. Two candidate keys conflict with one another.  
D. There are multiple foreign keys referencing the same primary key.

### 20.
Which statement best describes the process of joining two tables in a relational database?  
A. Tables are joined by combining their primary keys without using foreign keys.  
B. Tables are joined using an SQL operation (such as INNER JOIN) that links records based on matching foreign and primary key values.  
C. Joining tables automatically denormalizes the data.  
D. Tables can only be joined if they share the same structure and attributes.