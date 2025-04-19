### Written Answers

1. **Primary vs. Foreign Keys:** A primary key uniquely identifies each record within its own table. A foreign key holds values referring to another table’s primary key, enforcing referential integrity and modeling relationships (one‑to‑many or many‑to‑many).
     ^e5dec8
2. **Functional Dependency:** A functional dependency occurs when one attribute (or set) determines another’s value. It guides normalization by showing which attributes should be grouped to eliminate redundancy and anomalies.
     ^8f99a6
3. **1NF vs. 2NF vs. 3NF:** ^6dd0d5
    
    - **1NF:** Eliminates multi‑valued cells and repeating groups.
         ^ee7e8d
    - **2NF:** Removes partial dependencies; non‑key attributes must depend on the entire primary key.
        
    - **3NF:** Removes transitive dependencies; non‑key attributes depend only on the primary key.
        
4. **Library ER Diagram:** ^c6012e
    
    - **Entities:** Book(ISBN PK, Title, Publisher), Author(AuthorID PK, Name), Loan(LoanID PK, ISBN FK, MemberID FK, LoanDate).
        
    - **Relationships:** Author–Book 1–_; Book–Loan 1–_; Member–Loan 1–*.
        
5. **SQL SELECT with ORDER BY:**
    
    sql
    
    Copy
    
    `SELECT c.name, c.address FROM customers AS c JOIN rentals AS r   ON c.customer_id = r.customer_id WHERE r.rental_date BETWEEN '2025-01-01' AND '2025-03-31' ORDER BY r.rental_date;`
     ^65138c
6. **SQL Subquery for Non‑Ordering Customers:**
    
    sql
    
    Copy
    
    `SELECT name FROM Customers WHERE customer_id NOT IN (   SELECT customer_id   FROM Orders );`
     ^b4a4f0
7. **Purpose of Views:** Views are virtual tables defined by stored queries. They can restrict visible columns/rows.  
    _Example:_
    
    sql
    
    Copy
    
    `CREATE VIEW payroll_view AS   SELECT employee_id, name, salary   FROM employees; GRANT SELECT ON payroll_view TO payroll_clerk;`
     ^f75bc5
8. **ACID Properties:** ^da4057
    
    - **Atomicity:** All or nothing (bank transfer).
        
    - **Consistency:** Constraints upheld (no negative balances).
        
    - **Isolation:** No intermediate state visible (concurrent transfers).
        
    - **Durability:** Committed changes persist after crash (logged to disk).
        
9. **Concurrency & Locking:** Lost updates arise when two transactions overwrite each other. Share (read) locks allow multiple readers; exclusive (write) locks prevent others reading or writing. Two‑phase locking ensures serialisability.
     ^6f1dbd
10. **SQL Injection & Mitigation:** Attackers inject SQL via unvalidated inputs (e.g., `OR 1=1`). Mitigations: use parameterised statements and sanitize/escape inputs or employ stored procedures.
     ^f412bc
11. **Fragmentation vs. Replication:** ^073933
    
    - **Fragmentation:** Split data (e.g., by region) across sites.
        
    - **Replication:** Copy data (or full DB) to multiple sites for availability.
        
12. **Three Transparencies:** ^f289f4
    
    - **Fragmentation Transparency:** User unaware of fragments.
        
    - **Location Transparency:** User unaware of fragment locations.
        
    - **Replication Transparency:** User sees single logical copy despite replication.
        
13. **Homogeneous vs. Heterogeneous DDBMS:** ^87bcc2
    
    - **Homogeneous:** Same DBMS software/site; simpler integration.
        
    - **Heterogeneous:** Different DBMS/products; requires schema/format translation.
        
14. **CAP Theorem:** Under partition, you must pick Consistency or Availability. CP yields consistent but possibly unavailable service; AP yields available but potentially stale data.
    
15. **ACID vs. BASE:**
    
    - **ACID:** Strong transactional guarantees (atomic, consistent, isolated, durable).
        
    - **BASE:** Soft guarantees (Basically Available, Soft state, Eventual consistency) for high availability and partition tolerance.
        
16. **NoSQL Types & Use Cases:**
    
    - **Key‑Value:** Session stores (fast lookups).
        
    - **Document:** User profiles (flexible JSON).
        
    - **Column‑Family:** Time‑series analytics (wide tables).
        
    - **Graph:** Social networks (multi‑hop relationships).
        
17. **Embedding vs. Referencing in MongoDB:**
    
    - **Embedding:** Puts related data inline (fast reads; can bloat docs).
        
    - **Referencing:** Stores ObjectIDs and joins (keeps docs small; needs extra lookups).
        
18. **MongoDB Sharding, Replication & Indexing:**
    
    - **Sharding:** Distributes data across shards via shard key.
        
    - **Replica Sets:** Primary handles writes, secondaries replicate for failover/reads.
        
    - **Indexes:** Speed reads on indexed fields but add storage overhead and slow writes.
        
19. **Graph DB Shortest‑Path Pseudocode & Efficiency:**
    

cpp

Copy

`function shortestPath(start, goal):     queue = [(start, [start])]     visited = {start}     while queue:         node, path = queue.pop(0)         for nbr in node.neighbors():             if nbr == goal: return path + [nbr]             if nbr not in visited:                 visited.add(nbr)                 queue.append((nbr, path + [nbr]))     return null`

Graph DBs store adjacency natively, so traversals touch only relevant nodes/edges (no expensive joins).  
20. **Data Warehousing & Mining:**  
- **Data Warehouse:** Integrated, time‑variant, non‑volatile archive for analytics.  
- _Benefit:_ Historical trend analysis.  
- _Challenge:_ Complex ETL and storage cost.  
- **Data Mining:** Extracts unknown patterns (e.g., clustering) to inform decisions.

### Multiple Choice Answers

1. b
    
2. b
    
3. b
    
4. c
    
5. b
    
6. b
    
7. b
    
8. b
    
9. c
    
10. b
    
11. b
    
12. c
    
13. b
    
14. c
    
15. c
    
16. c
    
17. c
    
18. c
    
19. c
    
20. b