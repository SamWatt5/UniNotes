# The Aggregation Pipeline
In MongoDB, the Aggregation Pipeline allows you to process and analyze data through a series of stages. Each stage transforms the documents passing through it.
## Key Pipeline Stages
- `$match`: Filters documents to pass only those that meet specified criteria (similar to SQL's WHERE clause)
- `$group`: Groups documents by a key and performs aggregation operations (like counting, summing, averaging)
- `$sort`: Orders the aggregated or filtered documents
- `$project`: Reshapes each document by including, excluding, or computing new fields.
### Example
Imagine you have a collection of students and you want to group them by degree and count each group:
```js
db.students.aggregate([{
	$group: {
		_id: "$degree",
		total: { 
			$sum: 1
		}
	}
	}])
```
This pipeline performs a GROUP BY-like operation and counts how many students belong to each degree program.

# Schema Flexibility in NoSQL
While MongoDB is often described as "schema-less", it is more accurately described as **schema-flexible**. You still define a structure, your data model, to answer key questions, such as:
- **What does my application do?**
- **What data will I store?**
- **How will users access the data?**
- **What data is most valuable to me?**
These questions guide you to design documents that best suit your application's needs

# Embedding vs. Referencing: Modeling Relationships
Since NoSQL uses document storage, you must choose how to represent relationships between pieces of data. Two common approaches are **embedding** and **referencing**.
## Embedding
### What it is
Incorporating related data directly within a single document
### Advantages
- Retrieve all related information with a single query
- Simplifies updates and deletions because all information is contained in one place
### Ideal For
One-to-one relationships or when data is always accessed together
### Example
Inserting an author document and later embedding contact information:
```js
db.authors.insertOne({
	"first_name": "Sam",
	"last_name": "Watts",
	"dob": new Date("2005-01-27"),
	"books_published": 1,
	"active": true
})

db.authors.updateOne(
	{first_name: "Sam"},
	{ $set: {
		contact_info: {
			phone: "07443526226",
			email: "2508240@dundee.ac.uk",
			linkedin: "https://linkedin.com/in/SamWatt5"
		}	
	}}
)
```
## Referencing
### What it is
Storing relationships by including a reference (e.g. an ID) to a document in another collection.
### Advantages
- Avoids data duplication by keeping documents lean
- Ideal when related objects need to be updated independently
### Challenges
Retrieving all related data might require additional lookups (using the $lookup stage).
### Example
For a one-to-many relationship, such as an author with multiple books:
```js
db.authors.updateOne(
	{first_name: "Keith"},
	{$set: {
		books: ["0146003527", "0146001338", "0718138104"]
	}}
)

db.books.insertOne({"_id": "0146003527", title: "Cognac Cookery"})
db.books.insertOne({"_id": "0146001338", title: "Hot & Spicy Floyd"})
db.books.insertOne({"_id": "0718138104", title: "Floyd on Italy"})
```
Later, you can join the data using an aggregation with the $lookup stage.
# Rules and Considerations for Data modelling
- **Rule 1**: Favour embedding unless there is a strong reason not to
	- use embedding when related data is always accessed together
- **Rule 2**: Consider the independence of the data
	- If a piece of data needs to be accessed on its own, use referencing
- **Rule 3**: Balance the need for joins
	- Avoid joins if you can store related information together, but use $lookup if it leads to a more maintainable schema
- **Rule 4**: Prevent unbound array growth
	- Embedded arrays should not grow indefinitely to avoid performance issues
- **Rule 5**: Model based on application access patterns
	- Design your schema depending on whether your application is read-heavy or write-heavy
## Practical Example:
For a social media application:
- **Posts**: You might embed a few recent comments directly in the post document for fast display
- **Older or less frequently accessed comments**: These could be stored in a separate collection and referenced to avoid bloating the post document
