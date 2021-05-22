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

### RELIABILITY OR ACID COMPLIANCY

ACID stands for _Atomicity, Consistency, Isolation, and Durability_.

## SQL VERSUS NO-SQL - WHICH ONE TO USE?

### SQL REASONS

### NO-SQL REASONS
