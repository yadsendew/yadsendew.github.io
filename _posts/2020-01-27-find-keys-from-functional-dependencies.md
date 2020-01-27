---
layout: post
title: Find keys from functional dependencies
date: 2020-01-27 14:13 +0000
categories: "Database"
---
**Candidate key** is a minimal superkey.  
For those unfamiliar, a **superkey** is a set of attributes whose **_closure_** is the set of all atributes.  
The first step of finding **a candidate key**, is to find **all the superkeys**.  
## To find superkeys
For example the relation `R = {A, B, C, D, E}`  and following functional dependencies:  `A -> B` , `BC -> E` and `DE -> A`

**TRICK:** `for attributes do not appear in RHS of the FDs, every key must include them.`

Using above trick, **every key must include** both `C` and `D`.
    
**STEPS:**  
1. **Start** from **all** attributes. `Example: ABCDE`
2. **Remove** an attribute and see it is possible to **reinsert** using FDs.   
    `For example: we removed A from ABCDE then got BCED, and successfully reinserted it by using FD: DE -> A`
3. **If success**, we have a **superkey**.
4. **Repeat step 2** for **received superkey** to see if any more superkey?


**FULL EXAMPLE:**

All superkeys must contain `C` and `D`
* `ABCDE` (All attributes is always a super key)
* `BCDE` (Removed `A`. Reinsert `A` through `DE -> A`)
  * `CDE` (From `BCDE`. Remove `B`. Reinsert `B` from `A -> B`)
* `ACDE` (Removed `B`. Reinsert `B` through `A -> B`)
  *  `ACD` (From `ACDE`. Remove `E`. Reinsert `E` through `BC -> E`)
* `ABCD` (Removed `E`. Reinsert `E` through `BC -> E`)
  * `BCD` (From `ABCD`. Remove `A`. Reinsert A from `DE -> A`)
* Some set are not attributes:
  * `CD`: From `CDE`, remove `E` and cannot reinsert `E` from given FDs.