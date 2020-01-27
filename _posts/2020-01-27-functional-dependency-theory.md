---
layout: post
title: Functional Dependency Theory
date: 2020-01-27 00:35 +0000
categories: ["Database"]
---
![](/assets/img/2020-01-27-01-36-06.png)
## Amstrong's axioms 
![](/assets/img/2020-01-27-01-36-28.png)
## Additional rules
![](/assets/img/2020-01-27-01-36-53.png)
## Example
![](/assets/img/2020-01-27-01-38-19.png)
![](/assets/img/2020-01-27-01-39-37.png)
![](/assets/img/2020-01-27-01-37-54.png)

## Closure of attributes set
Say that B is **functional determined** by A if A -> B. To test whether A is superkey. Must devise an algorithm for computing the set of attributes functionally determined by A.  
One way of doing this is to compute F+ , take all functional dependencies with  as the left-hand side, and take the union of the right-hand sides of all such dependencies.
#### A procedure:
![](/assets/img/2020-01-27-01-44-16.png)
#### An efficient algorithm:
![](/assets/img/2020-01-27-01-51-14.png)
#### To illustrate how algorithm works, we use it to compute (AG)+
![](/assets/img/2020-01-27-01-54-28.png)