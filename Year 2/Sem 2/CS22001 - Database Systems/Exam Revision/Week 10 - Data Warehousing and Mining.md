# Overview and Rationale
## Context of Databases So Far
Traditional databases (OLTP (Online Transaction Processing) systems) were designed to handle relatively small, immediately current datasets. They focus on recording day-to-day transactions and are often "live", meaning old data may be overwritten. In contrast, modern business needs have shifted towards collecting and retaining massive amounts of data. This historical data holds potential for deeper analysis and improved decision-making, which is where data warehouses and mining come in.
## The Need for Data Warehousing
- **Volume and Variety**: Modern organizations collect data from many sources - both structured (e.g. numbers, text) and unstructured (e.g. images, video)
- **Time-Variance**: Instead of overwriting older facts, data warehouses save snapshots over time. This supports trend analysis and helps predict future events.
- **Decision Support**: Data warehouses serve as a "single source of truth" that supports management's decision-making process through Business Intelligence tools
# What is a Data Warehouse?
A data warehouse is defines as:
> "A subject-oriented, integrated, time-variant, and non-volatile collection of data in support of management's decision making process"
> - Bill Inmon, 1993
Let's break these components down:
## Subject-Oriented
- **Focus**: Data is organized around major subjects (e.g. customers, products, sales) rather than around individual application processes like invoicing or stock control
- **Advantage**: This makes it easier to analyze data across the key areas of a business
## Integrated
- **Data from Multiple Sources**: Data warehouses combine information from various operational systems
- **Unified View**: Since these systems may use different formats or standards, the data warehouse applies a transformation process to create consistency
## Time-Variant
- **Historic Records**: The warehouse stores data as a series of snapshots taken at different points in time
- **Trend Analysis** This time-based historical data is critical for identifying trends an supporting predictive models
## Non-Volatile
- **Stable Data**: Once data is entered into the warehouse, it is not updated or deleted. New data is added, leaving the historical records intact
- **Consistency for Analysis**: This feature ensures that analyses and reports reflect a stable, consistent dataset over time
# Data Warehouse Queries and Business Intelligence
Data warehouses support a range of query types, from relatively simple summary operations to very complex, multidimensional queries. The goal is to extract "wisdom" from the data. in Business Intelligence, these queries help answer strategic questions such as:
- "What was the total revenue for renting and sales in a specific quarter?"
- "Which areas are most popular based on historical renting data?"
- "How do current trends compare with past years?"
These queries are built on the massive historical dataset in the warehouse and often employ specialized OLAP tools to perform the following key operations:
# OLAP and Dimensional Operations
OLAP (OnLine Analytical Processing) enables flexible data analysis. Four primary operations are used to view data from different dimensions
## Roll-Up
- **Purpose**: Aggregate data by climbing up a dimensional hierarchy
- **Example**: Summing quarterly sales into annual totals, thereby reducing the level of detail.
## Drill-Down
- **Purpose**: The reverse of roll-up, it reveals the detailed data that lies beneath aggregated information
- **Example**: Breaking down an annual revenue figure into quarterly or monthly data
## Slice and Dice
- **Slice**: Selects a single dimension from the data to view a "slice" of the dataset
- **Dice**: Uses multiple dimensions to create a sub-cube for more complex analysis
- **Example**: Examining sales data for a specific product category (slice) or for that category in a particular region and timeframe (dice)
## Pivot (Rotate)
- **Purpose**: Change the orientation of the data view to provide alternative perspectives
- **Example**: Rotating rows into columns to compare data metrics from different angles

|Operation|What it does|Think of it like...|
|---|---|---|
|Roll-Up|Summarises / zooms out|Weekly → Monthly sales|
|Drill-Down|Gives more detail|Yearly → Monthly breakdown|
|Slice|Cuts one dimension|Chocolate sales only|
|Dice|Filters multiple dimensions|Chocolate + Dundee + Q1|
|Pivot|Rotates how data is shown|Flip rows and columns|
These operations enable analysts to explore data interactively, revealing patterns that might not be obvious in a static dataset
# Transition: From Data Warehousing to Data Mining
Once a data warehouse is established, organizations use data mining to uncover hidden patterns and trends. This process uses techniques from statistics and machine learning an typically involves:
## Data Mining Defined
Data mining is "the process of extracting valid, previously unknown, comprehensible, and actionable information from large databases." It is not a random search, it is guided by techniques designed to find statistically significant patterns.
## Key Data Mining Operations
### Predictive Modelling
- **Goal**: Use historical data to build models that predict future trends
- **Techniques**: Supervised learning methods such as classification (determining the category an object belongs to) and value prediction (forecasting numerical outcomes)
- **Examples**: Customer retention, credit approval decisions, direct marketing responses
### Database Segmentation
- **Goal**: Group similar records into clusters
- **Approach**: Typically uses unsupervised learning so that the system "discovers" sub-populations (e.g. customer profiles)
- **Application**: Tailored marketing campaigns or personalized healthcare recommendations
### Link Analysis
- **Goal**: Identify associations between records
- **Types**: 
	- **Association Discovery**: Finds "if-them" relationships (useful in market based analysis)
	- **Sequential Pattern Discovery**: Uncovers sequences of events over time
- **Application**: Product recommendation systems, for example, "if you liked this product, you might like that one"
### Deviation Detection
- **Goal**: Identify outliers or anomalies that deviate from expected norms
- **Application**: Fraud detection in financial transactions, quality control in manufacturing

|Operation|Goal|Example|
|---|---|---|
|🧠 Predictive Modelling|Forecast what will happen|“Will this user leave?”|
|🧩 Segmentation|Group similar things|“What customer types do I have?”|
|🔗 Link Analysis|Find connections & associations|“People who buy A also buy B”|
|🚨 Deviation Detection|Spot outliers|“Why is this transaction suspicious?”|
Each of these operations provides unique insights, transforming vast amounts of stored data into actionable knowledge that supports decision-making