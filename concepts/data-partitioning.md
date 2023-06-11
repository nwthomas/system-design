# DATA PARTITIONING 💽

Data partitioning is a technique to break up big database DBs into many smaller parts. It is the process of splitting up a DB/table across multiple machines to improve the manageability, performance, availability, and load balancing of an application. This is often used in conjunction with replication.

The justificiation for data partitioning is that, after a certain scale point, it is cheaper and more feasible to scale horizontally by adding more machines than to grow it vertically by adding beefier servers.

1. [Objectives of Partitioning](#objectives-of-partitioning)
2. [Partitioning Methods](#partitioning-methods)
   - [Horizontal Partitioning](#horizontal-partitioning)
   - [Vertical Partitioning](#vertical-partitioning)
   - [Directory-based Partitioning](#directory-based-partitioning)
3. [Partitioning Criteria](#partitioning-criteria)
   - [Key (or List-based) Partitioning](#key-or-list-based-partitioning)
   - [List Partitioning](#list-partitioning)
   - [Round Robin Partitioning](#round-robin-partitioning)
   - [Composite Partitioning](#composite-partitioning)
4. [Common Problems of Data Partitioning](#common-problems-of-data-partitioning)
   - [Joins and Denormalization](#joins-and-denormalization)
   - [Referential Integrity](#referential-integrity)
   - [Rebalancing](#rebalancing)

## OBJECTIVES OF PARTITIONING

We want:

1. A similar amount of data on each node
2. A similar amount of reads/writes on each node

If we can't get this, we end up with hot spots.

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

We would query the directory server to get where the data resides. This loosely-coupled approach means we can perform tasks like adding servers to the DB pool or changing our partitioning scheme without having an impact on the application.

## PARTITIONING CRITERIA

### KEY (OR HASH-BASED) PARTITIONING

In this scheme, we apply a hashing function to some key attributes of the entity we are storing; that yields the partition number. For example, if we have 100 DB servers and our ID is a numberic value that gets incremented by one each time a new record is inserted. In this example, the has could be `ID % 100` which will give us the server number where we can store/read that record.

This approach should ensure a uniform allocation of data among servers. The problem with it is that it fixes the total number of DB servers. Upgrading the number of servers changes the hashing function with requires redistribution of data, downtime for the service, and rebuilding the DBs.

A workaround is consistent hashing.

### LIST PARTITIONING

In this scheme, each partition is assigned a list of values, so whenever we want to insert a new record, we will see which partition contains our key and then store it there. For example, all users living in Iceland, Norway, Finland, or Denmark could be stored in the partition for Nordic countries.

### ROUND-ROBIN PARTITIONING

This simple strategy ensures uniform data distribution. With 'n' partitions, the 'i' tuple is assigned to partition `i % n`.

### COMPOSITE PARTITIONING

Under this scheme, we can combine any of the above to create a new scheme. For example, combining a list partitioning scheme and then a hash based one inside it. Consistent hashing could be considered a composite of hash and list paritioning where the hash reduces the key space to a size that can be listed.

## COMMON PROBLEMS OF DATA PARTITIONING

### JOINS AND DENORMALIZATION

Performing joins on a database which is running on one server is straightforward, but a partitioned one is not. Such joins will not be performance efficient since data has to be compiled from multiple servers. A common workaround for this problem is to denormalize the database so that queries that previously required joins can be performed from a single table. This means that the service will have to deal with the problems of denormalization (like data inconsitency).

### REFERENTIAL INTEGRITY

Enforcing data integrity constraints like foreign keys is extremely difficult. Most of the RDBMS do not support foreign key constraints across databases on different database servers. This means that the applications that require referential integrity on partitionined databases often have to enforce it in application code. Applications will also have to run regular SQL jobs to clean up dangling references.

### REBALANCING

Reasons for changing/rebalancing the data partitioning scheme include:

1. The data distribution is not uniform (e.g. there are a lot of places for a particular ZIP code that cannot fit into one database partition)
2. There is a lot of load on a partition, e.g., there are too many requests being handled by the DB partition dedicated to user photos

In such cases, either we have to create more DB partitions or have to rebalance existing partitions, which means that the partitioning scheme changed and all existing data moved to new locations.

Doing this without downtime is extremely difficult. Using a scheme like directory-based partitioning can make rebalancing a more palatable experience at the cost of increasing complexit of the system and creating a new single point of failure (i.e. the lookup service/database).
