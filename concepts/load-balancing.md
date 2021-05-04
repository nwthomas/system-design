# LOAD BALANCING

1. [Summary](#summary)
2. [Benefits of Load Balancing](#benefits-of-load-balancing)
3. [Load Balancing Algorithms](#load-balancing-algorithms)
4. [Redundant Load Balancers](#redundant-load-balancers)

## SUMMARY

Load Balancers (LBs) are a critical component of distributed systems which spread traffic across a cluster of servers to improve responsiveness and availability of applications, websites, or databases. LBs also keep track of the status of all the resources while distributing requests.

LBs will stop sending traffic to a node if its not avaialble to take a request, is not responding, has an elevated error rate, etc.

Load Balancers sit between the client and server (typically) and accepts incoming network and application traffice. It will then distribute the traffic across multiple back-end servers using various algorithms. This reduces individual server load and prevents any one application server from becoming a single point of failure, thus improving overall application availability and responsiveness.

![Load balancer](../assets/load-balancer.png)

We can use LBs in three spots:

1. Between the user and the web server
2. Between web servers and an internal platform layer (applications or cache servers)
3. Between internal platform layers and databases

![Load balancer use cases](../assets/load-balancer-use-cases.png)

## BENEFITS OF LOAD BALANCERS

The benefits of using a LB include faster, uninterrupted service. Users won't wait for a single server to finish its previous tasks. The user gets their requests back immediately from a ready resource.

Also, there's less downtime and higher throughput. A full server failure won't affect the end user experience as the load balancer will simply route new traffic to a healthy server.

LBs make it easier for system admins to handle incoming requests. Smart LBs have things like predictive analytics that determine traffice bottlenecks before they happen. These give an organization actional insights and can drive business decisions.

System admins experience fewer failed or stressed components when using LBs. Tons of devices get the workload distributed.

## LOAD BALANCING ALGORITHMS

There are two factors to consider when choosing a back-end server:

1. Ensuring that the server they choose is actually responding to requests
2. Using a pre-config algorithm to choose a server from the pool of healthy ones

### HEALTH CHECK

### LOAD BALANCING METHODS

## REDUNDANT LOAD BALANCERS
