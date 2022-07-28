# REPLICATION

Replication is having redundant copies of databases so that an application does not fail in the event of a crash. It also reduces load on each database serving requests.

## TABLE OF CONTENTS

- [Types of Replication](#types-of-replication)
- [Single Leader Replication](#single-leader-replication)
  - [Adding a Follower](#adding-a-follower)
  - [Dealing with a Follower Crash](#dealing-with-a-follower-crash)
  - [Dealing with a Leader Crash (Failover)](#dealing-with-a-leader-crash-failover)
  - [Problems with Failover](#problems-with-failover)
  - [Types of Single-Leader Replication](#types-of-single-leader-replication)
  - [Replication Log Implementation Options](#replication-log-implementation-options)
  - [Conclusion](#conclusion---single-leader-replication)
- [Multi-Leader Replication](#mutli-leader-replication)
  - [Conflict Avoidance](#conflict-avoidance)
  - [Last One Wins](#last-one-wins)
  - [On Read](#on-read)
  - [On Write](#on-write)
  - [Detecting Concurrent Writes](#detecting-concurrent-writes)
  - [Version Vectors](#version-vector)
  - [Conclusion](#conclusion---multi-leader-replication)
- [Leaderless Replication](#leaderless-replication)
  - [Keeping Data up to Date](#keeping-data-up-to-date)
  - [Conclusion](#conclusion---leaderless-replication-conclusion)

## TYPES OF REPLICATION

- Single Leader
- Multi-Leader
- No Leader

## SINGLE LEADER REPLICATION

### ADDING A FOLLOWER

Step 1: Intiialize the follower using a consistent snapshot of the leader database which is associated with some position in the replication log

Step 2: The follower can now begin accepting changes from the leader

### DEALING WITH A FOLLOWER CRASH

At time of crash, the follower knows where it was up to in the replication log

Step 1: On reboot, fetch all of the new changes from the leader node

Step 2: Start implementing the changes in the replication log from the index at which the follower node had previously failed

### DEALING WITH A LEADER CRASH (FAILOVER)

Step 1: Determine a new leader via some source of consensus (perhaps the most up to date replica)

Step 2: Configure all clients to send writes to new leader

Step 3: Configure all other followers to get changes from new leader

### PROBLEMS WITH FAILOVER

Some writes from the previous leader may have been propagated by only some or no replicas. This leads to either lost data or inconsistent replicas.

We can also have accidental failovers due to network congestion which can hurt our data base performance even more.

If the old leader comes back, we need to ensure that it does not think that it is the leader and continue to accept writes (resulting in a split brain).

### TYPES OF SINGLE-LEADER REPLICATION

- Synchronous
  - Client does not receive succss message until all replicas complete the write
  - Strong consistency
    Data is up to date, but writes take much longer
- Asyncronous
  - Client receives success message the second that master completes the write
  - Eventual consistency
  - Writes much faster, but clients can make stale reads to a replica

### REPLICATION LOG IMPLEMENTATION OPTIONS

- Copy over SQL statements
  - Bad because SQL statements are non-deterministic (for example, current time)
- Use internal write ahead log
  - Not scalable if changing database engine, says which bytes were changed, other databbase may have different data in different locations on disk
- Use logical log
  - Descrine which rows were modified and how, allows for more future proofing if the underlying databaxe engine changes in the future

### CONCLUSION - SINGLE LEADER REPLICATION

- Pros:
  - All writes go through one machine which ensures consistency across replicas
- Cons:
  - Since all writes have to go through one machine, write throughput may not be acceptable
  - Either need to partition the dataset and have a single leader per partition, or looks towards other replication strategies

## MUTLI-LEADER REPLICATION

### CONFLICT AVOIDANCE

The easiest way to deal with conflicts is to just avoid them. You do this by having all your writes to the same item go to a given leader.

However, this is not always possible if the leader is down or you want to change your database configuration.

### LAST ONE WINS

Each write is assigned a timestamp and writes with latest timestamp is kept.

It's very easy to implement, but the problem is that we don't know if we should use the client or server timestamp. Also, writes can be lost and clocks can skew on servers meaning that their times aren't perfectly synchronized.

### ON READ

When a database detects concurrent or conflicting values, store both writes. Then, return both values to a user on the next read to manually merge the values and store the resulting merged value in the database.

### ON WRITE

When a database detects concurrent writes, it calls a snippet of code to merge them somehow (often application-specific). This is the idea between conflict-free replicated types.

### DETECTING CONCURRENT WRITES

Two writes are concurrent if each client did not know about the write of the other when they made the write. it has nothing to do with actual time of write.

If one client knew about the write of the other, we would have a causality relationship between the two.

Hence, detecting concurrent writes is all about keeping track of what a client has seen from the database before making a write.

### VERSION VECTOR

Every time a client reads from the database, the database provides a version vector of a key.

Every time a client writes to a database, it passes the database its most recently read version vector for a key and the database supplies it with a new one.

Two values have a happens-before relationship if one version vector is strictly greater than the other.

If all other version vectors are concurrent, the corresponding values can either be merged somehow or kept as siblings in the database. The merging version means taking the max of both version vectors at every index.

### CONCLUSION - MULTI-LEADER REPLICATION

Pros:

- Can have a leader in each data center, makes having global service more manageable (outages between datacenters do not break application)
- Are not limited to the write throughput of a single node

Cons:

- Having to deal with write conflicts between multiple leaders

## LEADERLESS REPLICATION

Writes go to all databases nodes in parallel.

Reads go to all database nodes in parallel.

### KEEPING DATA UP TO DATE

1. Anti-Entropy
   - Background process that looks at multiple nodes and their stored values, use version numbers of the data in order to attempt to make sure that each replica holds the most up to date copy of the data
2. Read Repair
   - Since we are reading from multiple replicas in parallel, take the most up to dat piece of data and propagate it to the other replicas that had oudated data.
   - However, how can we guarantee that at least one of the replicas that we read from has the most up to date data?
3. Quoroms
   - Writes happen to all available nodes
   - Reads happen from all available nodes
   - If **w** nodes are written to and **r** nodes are read from and `w + r > n`, at least one of the nodes read from has writes and can read repair the others
   - Quorums are not perfect:
     - If we try to write to **w** nodes and it fails, the client is told it failed but the writes on nodes that did process are not undone
     - If you restore a failed node with an up to date value from one key using a node with an older value for that key, it will lose the up to date value
     - Can still have write conflicts
     - Sloppy quorums

### CONCLUSION - LEADERLESS REPLICATION CONCLUSION

- Pros:
  - Can work quite well in cross-datacenter solution
  - Have the quorum write parameter be small enough that all writes can go to one datacenter
- Cons:
  - Slower reads as result of multiple queries to nodes (with read repair)
  - Still have to reason about write conflicts
  - Quorums are not perfect, provide illusion of strong consistency when in reality this is often not true
