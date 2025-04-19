# MongoDB Indexes
Before diving into graph databases, lets discuss MongoDB indexes.
An index is a specialized data structure that speeds up data retrieval. It stores a subset of the document's fields along with pointers to the full documents. For example, running a query like: `db.movies.find({ runtime_min: { $gt: 200 } })` benefits from an index (created with something like `db.movies.createIndex({ runtime_min: -1 })`) because it allows the database engine to quickly look up records where the runtime meets the condition. 

# Graph Databases
Graph databases are designed to store data in the form of nodes and relationships (or edges):
- **Nodes (or vertices)**: These represent entities such as people, places, or objects
- **Edges (or links)**: These define the relationships between nodes, illustrating how entities connect
A graph is formally defines as a pair <V,E>, where V is the set of vertices and E is the set of edges connecting them.
The graph model is inherently different from how data is managed in relational databases. In graph databases, as the number of nodes increases, the "distance" (i.e. the connection path length) between nodes remains constant, meaning that related data is always just a few steps away, enabling very efficient joins and queries based on connectivity.
# Why Use Graph Databases
Graph databases are especially suited for scenarios where relationships are as important as the data items themselves. Some key benefits include:
- **Efficiency in Multi-hop Queries**
	- Because a graph database directly follows the stored edges, it only visits nodes that are connected
- **Natural Data Modeling for Networks**
	Graph Databases shine for social Networks, recommendation systems, or any domain where the relationships are dynamic and complex. They allow ad hoc data additions, meaning that you can easily add nodes and new relationships without needing to alter a rigid schema
- **Visualizability**
	Graph data can be visualized intuitively. For instance, many graph database management systems let you drag nodes, zoom in on connections, and explore patterns interactively
- **Real-Time Analytics**
	They are optimized for queries that span multiple "hops" or connections, making them ideal for real-time recommendations, pathfinding (such as shortest-path queries), and fraud detection
# Graph Database Use Cases and Query Examples
## Use Case 1: Social Networks
In social networks, users are nodes and "friendships" are edges. For example, you might want to find "Which games are played by the friends of User 1?"
- **Relational Approach**: This might require subqueries and multiple joins to match friends with game records.
```SQL
SELECT Name FROM Game  
WHERE GameID IN  
(SELECT GameID FROM GamesPlayers  
WHERE PlayerID IN  
(SELECT UserID2 FROM Friendship  
WHERE UserID1=1));  
```
- **Graph Approach**: You simply traverse from User 1's node through the "friend" relationships to the nodes representing game-playing activities. This traversal is direct and efficient because the relationships are stored explicitly.

```Pseudocode
FOR each friend IN UserA’s FRIENDS:  
FOR each game IN friend’s PLAYED games:  
ADD game to result_list  
RETURN result_list
```
## Use Case 2: Finding Common Interests
Another scenario might be finding users who have played both *Ocarina of Time* and *Skyrim*.
- **Relational SQL Example**: In a relational database, you'd perform multiple joins to combine records and filter by game names
```SQL
SELECT u.Username FROM User u  
JOIN GamesPlayers ug1 ON u.UserID = ug1.UserID  
JOIN Game g1 ON ug1.GameID = g1.GameID  
JOIN GamesPlayers ug2 ON u.UserID = ug2.UserID  
JOIN Game g2 ON ug2.GameID = g2.GameID  
WHERE g1.Name = 'Skyrim' AND g2.Name = Ocarina of Time';
```
- **Graph Model**: You check for users who have a "PLAYS" relationship to both game nodes. Pseudocode might iterate over each user, checking if both relationships exist, and then add those users to the result. This demonstrates how graph databases simplify queries where relationships matter. 
```Pseudocode
FOR each user IN User:  
IF user has "PLAYS" relationship to Game "Skyrim" AND  
user has "PLAYS" relationship to Game "Ocarina of Time":  
ADD user to result list  
RETURN result list
```
## Use Case 3: Shortest Path Queries
Consider a query to determine the shortest friendship path between two users:
- **Graph Approach**: You can use a breadth-first search starting from one node. As soon as the target node is reached, you output the path.
```Pseudocode
Use a breadth-first search to explore friends  
Track the path taken for each user.  
If we reach User B, return the path.  
If the queue is empty without finding User B, return "No  
path found".
```
- **Relational Approach**: Writing an equivalent SQL query would be extremely complex and inefficient compared to the natural iterative process in a graph database.
```SQL
God only knows! :\  
```
# Comparing Graph Databases and Relational Databases
## Performance
Graph databases are optimized for traversing relationships. In a relational model, finding interconnected data often requires multiple costly table joins, especially as the dataset grows.
## Data Modelling
While relational databases store data in tables (with foreign keys to represent relationships), graph databases model relationships directly as first-class citizens. This not only improves performance for connected data but often makes the data model simpler for problems that naturally map to a network.
## Query Expression
Rather than using complex SQL joins, graph query languages (like Cypher for Neo4j) let you express queries in a way that closely mirrors the natural relationships in your data. For example you might have a query structured like:
```Cypher
MATCH (u:User)-[:FRIEND_WITH]->(f:User)-[:PLAYS]->(g:Game)  
RETURN g.name
```
This reads almost like a sentence: "Find the game names played by friends of a user."
# Graph Database Tools
One popular graph database is **Neo4j**
- Developed around 2000 and available as open source since 2005
- Neo4j is widely used for handling complex and interconnected datasets because it is designed specifically for graph-like data structures
