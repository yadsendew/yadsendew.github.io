---
layout: post
title: Normal Forms and Normalization
date: 2020-01-28 20:24 +0000
categories: "Database"
---
## Second Normal Form Rules
**A relation schema is in 2NF if** **every** `nonprime attribute` **is** `fully functionally dependent` on `primary key`
* `nonprime attribute` and `primary key`
* `full functional dependency`: a FD Y -> Z where removal of any attribute from Y leads to the result does not hold anymore.
  * `{A, B} -> C` is **a full FD** since neither `A -> C` nor `B -> C` hold.
  * `{A, B} -> D` vis **partial dependency** since removed `B` but `A -> D` still hold
### Partial Dependency [YOUTUBE](https://youtu.be/39Gtyhn6DXg)
Subset of `primary key` (or `candidate key`) **determines** a `nonprime attribute`  
Example: `R = {A, B, C, D, E}`   
`F = {AB -> CD, B -> C, C -> D, D -> E}`  
[After finding closure](link), we have `AB+ = {A, B, C, D, E}`  
=> {A, B} is `candidate key` or `primary key`  
=> `prime attribute` = {A, B} and `nonprime attribute` = {C, D, E}  
Hence `B -> C` (`B` is subset of `primary key`, `C` is `nonprime attribute`) => Partial Dependency.  
**Hence, R is not in 2NF. We need to normalize as below:**
### Normalize
[Click here](http://www.mathcs.emory.edu/~cheung/Courses/377/Syllabus/9-NormalForms/2NF.html)