---
layout: post
title: Types of Schedule DBMS
date: 2020-02-10 19:05 +0000
categories: "Database"
---
This post is retrieved from [Geeksforgeeks.org](https://www.geeksforgeeks.org/types-of-schedules-in-dbms/)
<hr>

![](/assets/img/2020-02-10-20-07-00.png)
## Serial Schedules
Schedules in which the transactions are executed non-interleaved.  
[Example Picture](/assets/img/2020-02-10-21-21-04.png)
# Non-serial Schedules
## Serializable
* The non-serial schedule is said to be in a serializable schedule only when it is equivalent to the serial schedules, for an n number of transactions. 
* Since concurrency is allowed in this case thus, multiple transactions can execute concurrently. 
* A serializable schedule helps in improving both resource utilization and CPU throughput
  
These are of two types:
### Conflict Serializable
### View Serializable
## Non-serializable