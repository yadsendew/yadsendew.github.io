---
layout: post
title: Normal Forms and Normalization
date: 2020-01-28 20:24 +0000
categories: "Database"
---
### Second Normal Form Rules YOUTUBE
**A relation schema is in 2NF if** **every** `nonprime attribute` **is** `fully functionally dependent` on `primary key`
* `nonprime attribute` and `primary key`
* `full functional dependency`: a FD Y -> Z where removal of any attribute from Y leads to the result does not hold anymore.
  * `{A, B} -> C` is **a full FD** since neither `A -> C` nor `B -> C` hold.
  * `{A, B} -> D` is **partial dependency** since removed `B` but `A -> D` still hold