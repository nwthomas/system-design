# DESIGN A RATE LIMITER

A rate limiter is used in a network system to control the rate of traffic sent by a client or a service. This limits the number of client requests in HTTP sent over a specified period. All excess requests are usually blocked.

Example:

- Users can write no more than 2 posts per second per user
- You are capped at a max of 10 accounts per day from a given IP address
- You can claim rewards no more than 5 times per week from the same device

A rate limiter will prevent resources from being used up by DDoS attacks. Almost all production APIs by tech companies use some form of rate limiting. Google limits users to 300 read requests per 60 seconds.

Rate limiters also reduce costs, as it means you can depend on needed fewer resources for large bursts of activity.

Finally, rate limiting prevents your servers from being overloaded. To reduce server load, a rate limiter is used to filter extra requests by bots or user misbehavior.
