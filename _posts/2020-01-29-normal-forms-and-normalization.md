---
layout: post
title: Normal Forms and Normalization
date: 2020-01-29 19:01 +0000
categories: "Database"
---
 

Previous: [Functional Dependencies](link)  | Next: [Lossless and FD-preserving decomposition](link)
---------|----------
_This post is retrieved from [this](http://www.ict.griffith.edu.au/~jw/normalization/assets/Functional%20Dependencies%20and%20Normalization.pdf)_
<hr>

## Normal Forms
### Second Normal Form (2NF)
* _Definition 1_: In 2NF if for **every non-trivial FD** `A -> b`, **either** 
  * `A` is **not** a proper subset of any `candidate key`, **or**
  * `b` is a `key attribute`.
* _Definition 2_: In 2NF if there are no `non-key attributes` that are **partially dependent** on any `candidate key`.

### Third Normal Form (3NF)
* _Definition 1_: In 3NF if for **every non-trivial FD** `A -> b`, **either** 
    * `A` is a `superkey` , **or** 
    * `b` is a `key attribute`.

* _Definition 2_: In 3NF if it is already in 2NF, and there are no `non-key attributes` that are **transitively dependent** on any `candidate key`.

### Boyce-Codd Normal Form (BCNF)
* _Definition_: In BCNF if for **every non-trivial FD** `A -> b`, `A` is a `superkey`.

Clearly, **BCNF** > **3NF** > **2NF**.  
The above definitions also provide a way to test whether a table is in 2NF, 3NF or BCNF. One just needs to check each non-trivial FD to see whether it violates the definition of the normal forms.

## Normalization (_also called_ Decomposition)
### What is it?
When tables is **not in 2NF** (or 3NF, BCNF), we can **decompose** tables into smaller tables so that each of the smaller tables are in 2NF (or 3NF, BCNF). This process is called normalization.
### Approach:
For each FD `A -> b` that **violates** the normal form, we **decompose** `R` into `R1 = (A, b)`, and `R2=(R-{b})`. This process is **repeated until all tables are in the normal form**.  [See example](/assets/img/2020-01-29-20-36-34.png)  

<hr>

Previous: [Functional Dependencies](link) | Next: [Lossless and FD-preserving decomposition](link)
---------|----------