---
layout: post
title: Lossless and FD-preserving decomposition
date: 2020-01-29 19:38 +0000
categories: "Database"
---
## Definition
Suppose `R` is decomposed into smaller tables `R1,R2,…,Rn`. 
### Lossless
The decomposition is **lossless** if **any** instance `r` of `R`, `r` is equivalent to the natural join of its projections onto `R1, R2,... Rn`.  

### FD-preserving
If both `A` and `B` are attributes in `Ri`, and `A -> B` is implied by F, then `A -> B` is a FD that hold on `Ri`.  
**Decomposition is FD-preserving** if the **FDs that hold on** `R1, R2,…, Rn` altogether is equivalent to F.

### Remark
* Any table can be decomposed into 3NF tables with lossless-join property and FD-preserving property
* But we may not be able to decompose a table into BCNF with both of these properties.

### An algorithm for decomposing a table into 3NF with lossless and FD-preserving
1. Find the [minimal cover](https://yadsendew.github.io/database/2020/01/30/minimal-cover-of-a-set-of-functional-dependencies.html) of `F`. Suppose it is `E`.
2. For each FD `A -> b` in `E`, if `b` is a `non-key attribute`, have a table `(A,b)`, where `A` is the `primary key`.
3. _(optional)_ **Merge tables** that have **identical** `primary key`.
4. Have a table `R-B`, where `B` is the set of `non-key attributes` that **appeared on the RHS** of some FD in `E`.

#### Example:
![](/assets/img/2020-01-30-13-58-04.png)
