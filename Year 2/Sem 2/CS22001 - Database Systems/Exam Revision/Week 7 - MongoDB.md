## Document Data Model
### Structure of Data
- **Database**: The complete collection of data
- **Collections**: Groups of related documents
- **Documents**: Individual records that consist of key-value pairs
![[Pasted image 20250413145202.png]]
![[Pasted image 20250413145228.png]]
### Example Document
```json
{
	"name": "Melvin",
	"email": "melv@aol.com"
	// Additional fields as needed
}
```
### Embedding vs. Referencing
Documents can embed related information (e.g. a customer's purchase details) to support application-specific data access patterns
## Replication and Replica Sets
### Purpose of Replication
- Enhances availability and fault tolerance by maintaining copies of data
### Replica Set Overview (e.g. MongoDB)
- **Primary Node**: Handles all write operations (and by default, reads)
- **Secondary Nodes**: Continuously replicate data from the primary
- **Heartbeats**: Regular messages ensure that nodes are available
- **Automatic Election**: When the primary fails, a new primary is elected so that the system remains operational
### Benefits
- High availability - clients can still access data even if one or more nodes are down
## Sharding and Scalability
### Scaling Strategies
- **Vertical Scaling**: Upgrading a single server's resources (CPU, RAM) but with inherent limitations
- **Horizontal Scaling (Sharding)** Dividing data across multiple machines or nodes
### Sharding Details
#### Shard Key:
A critical field (or set of fields) used to determine the distribution of documents across shards
- A well-chosen shard key prevents hot partitions and ensures balanced load distribution
#### Use Cases
- Social media platforms (e.g. based on user ID or other evenly distributed values)
- IoT systems handling high volumes of sensor data
### Challenges
- Choosing the right shard key is crucial; a poor choice can lead to unbalanced shards and performance bottlenecks
## The aggregation Pipeline
### Purpose
Provides a powerful, multi-stage framework for processing and analyzing data within a document database
### Pipeline Stages
- `$match`: Filters documents based on specified criteria
- `$group`: Aggregated data (e.g. counts, sums) by grouping documents
- `$sort`: Orders the documents in the result
- `$project`: Specifies the fields to include or modify in the output
### Example Query
```json
db.students.aggregate([
	{$group: {_id: "$degree", total: {$sum: 1}}}
])
```
This example groups student documents by their degree and counts the total number of students in each group, similar to a grouped SQL query.
### Usefulness
The pipeline design allows combining multiple operations into a single, flexible query process that can handle complex data transformations

