# CACHING 💰

1. [Description](#description)
2. [Application Server Cache](#application-server-cache)
3. [Content Delivery (or Distribution) Network (CDN)](#content-deliver-or-distribution-network-cdn)
4. [Cache Invalidation](#cache-invalidation)
5. [Cache Evication Policies](#cache-evication-policies)

## DESCRIPTION

While Load Balancers help you scale horizontally across an increasing number of servers, caching will enable you to make vastly better use of the resources you already have as well as making other unattainable product requirements possible.

Caching makes create use of the _locality of reference principle_ - recently requested data is likely to be requested again. They are used in almost every computing layer: hardware, operating systems, web browsers, web applications, and more.

A cache is like a short-term memory: it has a limited amount of space, but is typically faster than the original data source and contains the most recently accessed items (like the least-recently used - LRU - cache type).

Caches are typically found in all levels of architecture, but are more likely to be present towards the front-end. This is because they can return taxing data quickly without using downstream resources.

## APPLICATION SERVER CACHE

Placing a cache directly on a request layer node enables the local storage to upgrade its response time. The node will just return locally cached data if it exists instead of queries the data store. This could be in memory on on disk storage (which is still much faster than going to the network storage).

If you have many nodes and the LB distributes the requests across them, this will cause problems for the caches as it will exponentially increase cache misses. You can either use a global cache or distributed caches.

## CONTENT DELIVERY (OR DISTRIBUTION) NETWORK (CDN)

A CDN will get a request, check if it has it locally, and then request it from the back-end servers and stash it before sending it on. Subsequent requests will be faster.

If the system we're building isn't big enough to have its own CDN, we can just host the file on a lightweight HTTP server light Nginx and then cut over the DNS from the servers to a CDN later.

## CACHE INVALIDATION

Caching requires some logic to keep the cache orderly and in parallel with the cache. If we don't do this, we can get wildly inconsistent application behavior.

There are three main ways to do cache invalidation:

1. **Write-through cache** - Data that is written into the cache and the corresponding DB happen simulataneously. The cached data allows for fast retrieval and, since the same data gets written to permanent storage, we have complete data consistency at all times whenever data is modified. This also increases consistency in the event of a emergent event like a power failure.
2. **Write-around cache** - Data is written directly to permanent storage and bypasses the cache. While this reduces flooding the cache with a ton of write tasks that will never be read, the disadvantage is that a read request for recently written data will create a "cache miss" and have to be read from the back-end storage/database with higher latency.
3. **Write-back cache** - Data is written to the cache alone, and completion is immediately confirmed to the client. Then, a write happens to the permanent storage afterwards with specified intervals and under certain conditions. This is very low-latency and has high-throughput for write-intensive applications, but we now have a risk of data loss if there's a crash and our cache goes down. The only copy of the written data, until the write to the database, is in the cache.

## CACHE EVICTION POLICIES

A cache evication policy is how the cache will invalidate/evict data:

- FIFO, or First in, First out: The cache evicts the first block of data accessed first without any regard to how often or how many times it was accessed before.
- LIFO, or Last in, Last out: The cache gets rid of the most recently-accessed data without any regard to how often or how many times it was used ebefore.
- LRU, or Least Recently Used: Discards the least recently used items first.
- MRU, or Most Recently Used: Discards the most recently used items first.
- LFU, or Least Frequently Used: Counts how often an item is needed. Those that are used least often are discarded first.
- RR, or Random Replacement: Randomly selects a candidate item and then discards it to make space when necessary.

[Additional Content](https://lethain.com/introduction-to-architecting-systems-for-scale/)
