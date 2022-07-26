# REPLICATION

Replication is having redundant copies of databases so that an application does not fail in the event of a crash. It also reduces load on each database serving requests.

## TABLE OF CONTENTS

- [Adding a Follower](#adding-a-follower)
- [Dealing with a Follower Crash](#dealing-with-a-follower-crash)
- [Dealing with a Leader Crash (Failover)](#dealing-with-a-leader-crash-failover)
- [Problems with Failover](#problems-with-failover)
- [Types of Single-Leader Replication](#types-of-single-leader-replication)

## ADDING A FOLLOWER

Step 1: Intiialize the follower using a consistent snapshot of the leader database which is associated with some position in the replication log

Step 2: The follower can now begin accepting changes from the leader

## DEALING WITH A FOLLOWER CRASH

At time of crash, the follower knows where it was up to in the replication log

Step 1: On reboot, fetch all of the new changes from the leader node

Step 2: Start implementing the changes in the replication log from the index at which the follower node had previously failed

## DEALING WITH A LEADER CRASH (FAILOVER)

Step 1: Determine a new leader via some source of consensus (perhaps the most up to date replica)

Step 2: Configure all clients to send writes to new leader

Step 3: Configure all other followers to get changes from new leader

## PROBLEMS WITH FAILOVER

Some writes from the previous leader may have been propagated by only some or no replicas. This leads to either lost data or inconsistent replicas.

We can also have accidental failovers due to network congestion which can hurt our data base performance even more.

If the old leader comes back, we need to ensure that it does not think that it is the leader and continue to accept writes (resulting in a split brain).

## TYPES OF SINGLE-LEADER REPLICATION

- Synchronous
  - Client does not receive succss message until all replicas complete the write
  - Strong consistency
    Data is up to date, but writes take much longer
- Asyncronous
  - Client receives success message the second that master completes the write
  - Eventual consistency
  - Writes much faster, but clients can make stale reads to a replica
