# SQL VERSUS NO-SQL 💽

1. [Summary](#summary)
2. [SQL](#sql)
3. [NoSQL](#nosql)
   - [Key-Value Stores](#key-value-stores)
   - [Document Databases](#document-databases)
   - [Wide-Column Databases](#wide-column-databases)
   - [Graph Databases](#graph-databases)
4. [High Level Differences Between SQL and NoSQL](#high-level-differences-between-sql-and-no-sql)
   - [Storage](#storage)
   - [Schema](#schema)
   - [Querying](#querying)
   - [Scalability](#scalability)
   - [Reliability or ACID Compliance](#reliability-or-acid-compliance)
5. [SQL versus NoSQL - Which one to use?](#sql-versus-no-sql-which-one-to-use)
   - [SQL Reasons](#sql-reasons)
   - [NoSQL Reasons](#no-sql-reasons)

## SUMMARY

In the world of databases, there are really two main types of solutions on the market - SQL and NoSQL, or Relational or Non-Relational Databases.

Both of these differ in the _reasons_ and _way_ they were built, the information they store, and the way that they store that data.

Relational databases were structured to have predefined schemas like phone books that store phone numbers and addresses.

Non-relational databases are unstructured, distributed, and have a dynamic schema like file folders that hold everything from a person's address and phone number to their Facebook "likes" and online shopping preferences.

## SQL

SQL or relational databases store data in rows and columns. Each row contains all the information that is needed about an entityt while each column is a separate data point. Some of the most popular RDs include MySQL, Oracle, MS SQL Server, SQLite, Postgres, and MariaDB.

## NO-SQL

These are different types of NoSQL Databases ⤵️

### KEY-VALUE STORES

Data is stored in an array of key-value pairs. The key is an attribute name which is linked to a value. Well-known key-value stores include REdix, Voldemort, and Dynamo.

### DOCUMENT DATABASES

In document databases, data is store in documents (instead of rows and columns) and are grouped together in collections. Each document can have an entirely different structure. Document databases include CouchDB and MongoDB.

### WIDE-COLUMN DATABASES

Instead of tables, wide-column databases have column families which are containers for rows. Unlike relational databases, we don't need to know all the columns up front and each row doesn't have to have the same number of columns. These types of databases are best suited for analyzing large datasets - big names include Cassandra and HBase.

### GRAPH DATABASES

These are used to store data whose relations are best represented in a graph. Data gets saved into graph structures with the nodes/vertices/entities, properties (which are the information about the entities), and lines/edges. Examples of graph databases include Neo4J and InfiniteGraph.

## HIGH LEVEL DIFFERENCES BETWEEN SQL AND NO-SQL

### STORAGE

SQL stores data in tables where each row represents an entity and each column represents a data point about that entity. For example, a car entity would have coluns with Color, Make, Model, etc.

NOSQL DBs have key-value, document, graph, and columnar schemas.

### SCHEMA

In SQL, each record conforms to a fixed schema meaning that the columns must be decided and chosen before data entry and each row must have data for each column. The schema can be updated later, but it means modifying the entire DB and taking it offline (e.g. "Maintenance").

In contrast, NoSQL DBs have schemas that are dynamic. Columns can be added on the fly and each 'row' doesn't have to necessary have data for each column.

### QUERYING

SQL databases use SQL (Structured Query Language) for defining and manipulating data. It's _extremely_ powerful.

In NoSQL, queries are focused on a collection of documents. This is also sometimes called UnQL (Unstructured Query Language). Different DBs have different syntax for using UnQL.

### SCALABILITY

In most situations, SQL DBs are vertically scalable (increasing horsepower) which is really expensive. It's possible to scale a relational DB across multiple servers, but this is challenging and time-consuming.

In contrast, NoSQL databases are horizontally scalable which means that we could add more servers to our NoSQL DBs infrastructure to handle more traffic. Any cheap commodity hardware or cloud instances can host NoSQL databases, so it's a lot more cost-effective than vertical scaling. A lot of these NoSQL technologies distribute data across servers automatically.

### RELIABILITY OR ACID COMPLIANCY

ACID stands for _Atomicity, Consistency, Isolation, and Durability_.

Most relational databases are ACID compliant. There's a safe guarantee of performing transactions that there will be data reliability.

In contrast, most NoSQL solutions sacrifice ACID compliance for performance and scalability.

## SQL VERSUS NO-SQL - WHICH ONE TO USE?

Most business have both relational and non-relational DBs for different needs. As NoSQL is gaining popularity for speed and scalability, there are situations were a highly structured SQL DB may perform better; choosing the right technology depends on the use case.

### SQL REASONS

You should choose a SQL database if:

1. We need ACID compliance. This will protect the data in the database by prescribing exactly how transactions interact with the database. Many e-commerce and financial applications need ACID compliance.
2. Your data is structured and unchanging. If your business is not experiencing massive growth that would require more servers and if you're only working with data that is consistent, then there may be no reason to have a system that supports a variety of types of data and traffic.

### NO-SQL REASONS

NoSQL databases prevent data from being the bottleneck. Big data needs NoSQL databases because it handles data differently than the traditional relational databases.

You should choose a NoSQL database if:

1. You need to store large amounts of data that have little-to-no structure. There's no limits on the types of data that we can store together, so NoSQL allows us to add new types as the need changes. You can store your data in one place without having to define what types of data those are in advance or take your database down for it.
2. You need to make the most of cloud computing and storage.
3. You are undergoing rapid development. NoSQL is useful for this because it doesn't need to be prepped ahead of time. If you're making frequent updates to the data structure and need to maintain uptime, a relational database will slow you down.
