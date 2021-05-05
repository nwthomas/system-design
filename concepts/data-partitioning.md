# DATA PARTITIONING 💽

Data partitioning is a technique to break up big database DBs into many smaller parts. It is the process of splitting up a DB/table across multiple machines to improve the manageability, performance, availability, and load balancing of an application. The justificiation for data partitioning is that, after a certain scale point, it is cheaper and more feasible to scale horizontally by adding more machines than to grow it vertically by adding beefier servers.

1. [Partitioning Methods](#partitioning-methods)
   - [Horizontal Partitioning](#horizontal-partitioning)
   - [Vertical Partitioning](#vertical-partitioning)
   - [Directory-based Partitioning](#directory-based-partitioning)
2. [Partitioning Criteria](#partitioning-criteria)
   - [Key (or List-based) Partitioning](#key-or-list-based-partitioning)
   - [List Partitioning](#list-partitioning)
   - [Round Robin Partitioning](#round-robin-partitioning)
   - [Composite Partitioning](#composite-partitioning)
3. [Common Problems of Data Partitioning](#common-problems-of-data-partitioning)

## PARTITIONING METHODS

There are lots of schemes one could use to break a DB into many DBs. These are three of the most popular ones:

### HORIZONTAL PARTITIONING

In this method, we put rows into different tables. If we are storing different places in a table, we can decide that locations with ZIP codes less than 10000 are stored in one table and greater than 10000 are stored in another. This is called range-based partitioning as we are storing different ranges of data. Horizontal partitioning is also called "Data Sharding."

The problem with this is that, if the value whose range is used for partitioning isn't chosen carefully, the sheme will lead to unbalanced servers where one group of range is highly overweight.

The example of ZIP codes assumes that there's an equal distribution of ZIP codes across both ranges. There will be lots of difference between ZIP codes from Mississippi and NYC.

### VERTICAL PARTITIONING

In this setup, we divide our data to store tables related to specific featuress in their own server. For an Instagram App, we an place user profile information on one DB server, friend lists on another, and photos on a third.

This is straightforward to implement and lends itself nicely to distributed systems/microservices, but the problem is that additional growth will require further partitioning a specific DB across various servers anyways.

### DIRECTORY-BASED PARTITIONING

A loosely-coupled approach to work around the issues with the two methods above is to create a lookup service which knows your current partitioning scheme and abstracts it away from the DB access code.

We would query the irectory server to get where the data resides. This loosely-coupled approach means we can perform tasks like adding servers to the DB pool or changing our partitioning scheme without having an impact on the application.

## PARTITIONING CRITERIA

### KEY (OR HASH-BASED) PARTITIONING

### LIST PARTITIONING

### ROUND-ROBIN PARTITIONING

### COMPOSITE PARTITIONING

## COMMON PROBLEMS OF DATA PARTITIONING
