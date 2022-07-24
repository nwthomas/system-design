# REPLICATION

Replication is having redundant copies of databases so that an application does not fail in the event of a crash. It also reduces load on each database serving requests.

## TABLE OF CONTENTS

- [Adding a Follower](#adding-a-follower)
- [Dealing with a Follower Crash](#dealing-with-a-follower-crash)
- [Dealing with a Leader Crash (Failover)](#dealing-with-a-leader-crash-failover)

## ADDING A FOLLOWER

Step 1: Intiialize the follower using a consistent snapshot of the leader databas which is associated with some position in the replication log

Step 2: The follower can now beging accepting changes from the leader

## DEALING WITH A FOLLOWER CRASH

At time of crash, the follower knows where it was up to in the replication log

Step 1: On reboot, fetch all of the new changes from the leader node

Step 2: Start implementing the changes in the replication log from the index at which the follower node had previously failed.

## DEALING WITH A LEADER CRASH (FAILOVER)

Step 1: Determine a new leader via some source of consensus (perhaps the most up to date replica)

Step 2: Configure all clients to send writes to new leader

Step 3: Configure all other followers to get changes from new leader
