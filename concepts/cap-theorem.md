# CAP THEOREM 🎩

1. [Summary](#summary)
2. [Consistency](#consistency)
3. [Availability](#availability)
4. [Partition Tolerance](#partition-tolerance)

## SUMMARY

The **CAP Theorem** states that it is impossible for a distributed system to simultaneously provide more than two out of three of the following guarantees (CAP) - Consistency, Availability, and Partition Tolerance.

Trading off among CAP is almost the first thing we want to consider.

![CAP Theorem](../assets/cap-theorem.png)

## CONSISTENCY

All nodes see the data at the same time. This is achieved by updating several nodes before allowing further reads.

## AVAILABILITY

Every request gets a response on success/failure. Availability is achieved by replicating the data across different servers.

## PARTITION TOLERANCE

The system continues to work despite message loss or partial failure. The system can sustain any amount of network failure and doesn't result in the entire system failing. Data is sufficiently replicated across nodes and networks to keep the system up through intermittent outages.

## DEALING WITH EVENTUAL CONSISTENTCY

Problems:

1. Reading your own writes (don't see write after just making it)
   - Solutions:
     - Always read from leader for editable for editable areas of application
     - Always read from the leader or up to date replicate for some period after a client write
2. Monotonic reads (reads look like they are going back in time - this is fixed by having each user read from the same replica)
   - Solutions:
     - Have same user read from same replica every single time
3. Consistent prefix reads (causal relationship between writes lost because )
   - Solutions:
     - Get all given messages up to a given timestamp on a given database
     - Have same user read from same replica every single time
