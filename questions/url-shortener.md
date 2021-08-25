# URL SHORTENER 🩳

This will be a service like TinyURL, bit.ly, goo.gl, qlink.me, etc. It will aliase and redirect to long URLs.

Difficulty: _Easy_

## TABLE OF CONTENTS

1. [Why do we need URL shortening?](#why-do-we-need-url-shortening)
2. [Requirements and Goals of the System](#requirements-and-goals-of-the-system)
3. [Capacity Estimation and Constraints](#capacity-estimation-and-constraints)
4. [System APIs](#system-apis)
5. [Database Design](#database-design)
6. [Basic System Design and Algorithm](#basic-system-design-and-algorithm)
7. [Data Partitioning and Replication](#data-partitioning-and-replication)
8. [Cache](#cache)
9. [Load Balancer (LB)](#load-balancer-lb)
10. [Purging and DB Cleanup](#purging-and-db-cleanup)
11. [Telemetry](#telemetry)
12. [Security and Permissions](#security-and-permissions)

## WHY DO WE NEED URL SHORTENING?

URL shortening is useful to gain "short links" that redirect to longer ones.

These short links are effectively aliases and save a _ton_ of space when posting/tweeting/etc. Users are also less likely to type in the wrong characters when using shorter links.

They are also useful to track clicks/user engagement with content.

## REQUIREMENTS AND GOALS OF THE SYSTEM

> 🚧 _ALWAYS CLARIFY REQUIREMENTS AT THE START_ 🚧

Our system has the following requirements:

**Functional Requirements**

1. Given a URL, our system should generate a unique and shorter version of it. This is called a short link. It should be easily copied and pasted into other applications.
2. When users access this link, it will redirect them to the original link.
3. Users should be able to optionally choose a custom short link.
4. Links should expire after a default timespan, but users should be able to override and specify an expiration time.

**Non-Functional Requirements**

1. The system should be highly available. Redirects cannot fail.
2. URL redirection should happen quickly, in real-time, and with minimal latency.
3. Shortened links should not be guessable.

**Extended Requirements**

1. Analytics would be nice (e.g. how many times redirects have happeneds)
2. Our service should be accessible through REST or other services

## CAPACITY ESTIMATION AND CONSTRAINTS

Our system is read heavy since users will create a shortened URL once and it could be read hundreds or thousands of times.

We can assume 100 read to 1 write scenario - 100:1.

If we assume 500M new URls per month, we can expect 50B redirects.

We will have about 193 new URLs created per second:

```
500000000 / (30 * 24 * 3600) = ~193/s
```

Based on our estimations before about redirect-to-write being 100:1, the redirects per second will be estimated at 19,300:

```
193 * 100 = 19,300/s
```

Our system will also have to store data. Let's assume that we store every URL shortening request for 5 years. Since we expect to have 500M new URLs every month the total number of objects we expect to store will be 30 billion:

```
500M * 5 years * 12 months = 30 billion
```

If we assume that each stored object will be approximately 500 bytes, we'll need 15 TB of total storage across 5 years:

```
30 billion * 500 bytes = 15 TB
```

We can estimate for bandwidth that we expect 300 new URLs as write requests per secton, with total incoming data of

## SYSTEM APIS

## DATABASE DESIGN

## BASIC SYSTEM DESIGN AND ALGORITHM

## DATA PARTITIONING AND REPLICATION

## CACHE

## LOAD BALANCER (LB)

## PURGING AND DB CLEANUP

## TELEMETRY

## SECURITY AND PERMISSIONS

```

```
