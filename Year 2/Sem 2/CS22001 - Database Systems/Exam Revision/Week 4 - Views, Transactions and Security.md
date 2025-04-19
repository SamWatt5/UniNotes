## Database Planning
### Purpose and Importance
Database planning is about establishing the framework for developing a database in line with the overall information systems (IS) strategy. It includes defining your mission and objectives so that the database can support the real needs of your organization or application. Planning covers:
- Defining a **mission statement** to clarify the purpose of the project
- Setting **mission objectives**, where each objective pinpoints a specific task or process the database must support
- Answering key questions such as:
	- What is the scope of the system?
	- Will you build and deploy the entire database at once or in stages?
	- How should the design and implementation be coordinated given the available resources, timescales, and budgets?
This stage also involves setting up standards for data collection, documentation, physical storage (such as local versus cloud solutions), and backup strategies. These points are crucial because they help ensure that the database not only fits the current needs but is also robust enough t support future requirements
## User Views
### Definition and Purpose
A user view is essentially a virtual table tailored to the needs of different user roles (e.g., managers, supervisors) or application areas. While the underlying database contains all the data, views serve two main purposes:
- **Customization**: They display only the parts of the data that are relevant for a particular user or role.
- **Security**: They restrict access to sensitive data - only approved information is made visible to the user
### Approaches to managing Multiple views
There are three main approaches to integrating multiple user views:
- **Centralised Approach**: Merge the requirements from all user views into one set of requirements. The single integrated data model represents all the user views
- **View Integration Approach**: Maintain separate lists of requirements for each view and merge the separate data models later
- **Combined Approach**: A blend where some common requirements are merged, while others are kept separate
## Transactions
### What Is a Transaction?
A transaction is defined as a logical unit of work in the database, meaning it consists of one or more operations that must all be completed successfully to maintain data integrity. 
A good example of this is to consider a bank transfer. When you transfer money, the transaction must either completely succeed, or fail entirely - you wouldn't want your money to disappear halfway.
The key characteristics of transactions are captured by the ACID properties:
- **Atomicity**: The entire transaction is performed, or none of it is (all or nothing). If one part of the transaction fails (say, in an online purchase, the payment doesn't go through), the entire transaction is rolled back so that nothing is partially completed
- **Consistency**: The database transitions from one valid state to another, maintaining all defined rules and constraints.
- **Isolation**: Intermediate states of the transaction are not visible to other users or transactions. This means that even if multiple transactions are occurring at once, each transaction should operate independently, as though it were the only one running. This prevents "dirty reads", where one transaction sees uncommitted changes from another
- **Durability**: Once a transaction is committed, its changes persist even if subsequent failures occur.
### Practical SQL Concepts
There are SQL commands for these, such as
- `START TRANSACTION`: Marks the beginning
- `COMMIT`: Ends the transaction and makes changes permanent
- `ROLLBACK`: Reverses all changes if something goes wrong
Imagine editing a document where you frequently press "save" (commit) to ensure nothing is lost, but you can also "undo" (rollback) if you make an error

## Transaction Concurrency
### The Challenge of Multiple Users
In a busy system like an online shop, many users might try to update the same record simultaneously (e.g. purchasing the last available item). This concurrency can lead to issues if not managed properly
### Common Concurrency Issues
- **Lost Update**: Two transactions update the same record, and one overwrites the other
- **Uncommitted Dependency**: One transaction reads data that another is still in the process of writing
- **Deadlock**: Two transactions each wait for resources held by the other, causing a standstill
### Locking and Two-Phase Locking (2PL)
To manage these issues, databases use **locking**:
- **Shared (Read) Locks**: Multiple transactions can read the same data simultaneously
- **Exclusive (Write) Locks**: Ensure that when a transaction is updating data, no other transaction can read or write that same data until the lock is released
In **Two-Phase Locking**, a transaction first acquires all the locks in needs (growing phase) and then, after completing the processing, releases all locks (shrinking phase). This method is like packing up all the tools you need before starting a repair job and then putting them all away at the end, ensuring that nobody else interferes until you're finished

## Database Security
### Why is Database Security Crucial?
Data in a database can be extremely valuable - and a target for various threats.
### Core Security Objectives
- **Confidentiality**: Ensuring that sensitive data is accessed only by those who are allowed, for instance, personal details or financial figures must remain hidden from unauthorized users.
- **Integrity**: The accuracy of data must be maintained. This means preventing unauthorized updates or corruption of the data.
- **Availability**: Authorized users must be able to access the data reliably, even in the event of hardware failures or attacks
### Threats and Countermeasures
#### Threats
Data can be compromised by external hackers via methods like SQL injection - where a malicious actor inputs harmful code into a query - or by internal mistakes or malicious insiders
#### Countermeasures
- **Access Controls**: Using SQL's `GRANT` and `REVOKE` commands to specify who can perform what action.
- **Encryption**: Both for storing data and for transmitting it over networks. This ensures that even if data is intercepted, it remains unreadable without the key
- **Backup and Recovery**: Regular backups and transaction logs allow you to recover the database in case of a failure or security breach
- **Safeguards Against SQL Injection**: By using parameterized queries and thoroughly sanitizing inputs, you prevent attackers from inserting harmful SQL code