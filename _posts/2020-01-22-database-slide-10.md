---
layout: post
title: Database Slide 10 - Functional Dependencies and Normalization for Relational Databases
date: 2020-01-22 15:56 +0000
categories: ["Database"]
ordered: true
---
[Link bài viết chi tiết và dễ hiểu](https://www.brainkart.com/article/Informal-Design-Guidelines-for-Relation-Schemas_11495/)
# Intro
**Relational database design** = the way of **grouping of attributes** to form **"good" relation schemas**  
Two levels of relational schemas:
* Logical "user view" level
* Storage "base relation" level  

The design is concerned mainly with **base relations**
* We will discuss **_four informal guidelines_** that may be used as **measures** to determine the **quality of relation schema design**  
* Then discussing the **_formal theory of relational database design_**


# Four informal guidelines for a "good" Relational Databases Design
## Semantics of the _**Relation Attributes**_
In general, **the easier** it is to explain the semantics of the relation, **the better** the relation schema design will be.

**Guideline 1:** each tuple should represent one entity or relationship instance (Applies to individual relations and their attributes)
* Attributes of different entities should not be mixed in the same relation
* Only foreign keys should be used to refer to other entities
* Entity and relationship attributes should be kept apart as much as possible.

**Bottom line (kết quả là):** a schema can be **easily explained relation** by **relation**. The **semantics of attributes** should be **easy to interpret**.


## Reducing the redundant information in tuples & update anomalies
**Problem:**
* Information is stored redundantly
    * Wastes storage 
    * Causes problems with [update anomalies](/assets/img/2020-01-23-01-25-36.png)
      * [Insertion anomalies](/assets/img/2020-01-23-01-25-57.png)
      * [Deletion anomalies](/assets/img/2020-01-23-01-26-33.png)
      * Modification anomalies


**GUIDELINE 2:**
* Design a schema that does not suffer from the insertion, deletion and update anomalies.
* If there are any anomalies present, then note them so that applications can be made to take them into account.


## Reducing the NULL values in tuples
**GUIDELINE 3:**

* Relations should be designed such that **their tuples** will **have as few NULL values as possible** 
* Attributes that are **NULL frequently** could be placed in **separate relations** (with the **primary key**)

**Reasons for nulls:**

* Attribute not applicable or invalid 
* Attribute value unknown (may exist) 
* Value known to exist, but unavailable

## Spurious Tuples (Tuple giả)
* Bad designs: for certain JOIN operations, it results error.
* The "lossless join" property is used to **guarantee meaningful results** for join operations

**Guideline 4:**
* The relations design **satisfies** the **lossless join condition** (no spurious tuples are generated)
* **No spurious tuples** should be **generated** by **natural-join** of any relations.

### There are two important properties of decompositions:

    a. Non-additive or losslessness of the corresponding join
    b. Preservation of the functional dependencies.

**Note that:**  
Property (a) is **extremely important** and **cannot be sacrificed**.  
Property (b) is **less stringent** and **may be sacrificed**. (See Chapter 11).
# Functional dependencies. [Guru99 FDs](https://www.guru99.com/dbms-functional-dependency.html)
* FDs:
  * Used to **specify formal measures** of the **"goodness" of relational designs** 
  * And **keys** are used to **define normal forms** for relations 
  * **Are constraints** that are **derived from the meaning and interrelationships** of the data attributes  
* A _set of attributes X_ **functionally determines** a _set of attributes Y_ **if** the _value of X_ **determines** a _unique value for Y_.  

[ FDs more + example](/assets/img/2020-01-23-13-02-02.png)

## [Inference Rules for FDs (Luật suy luận cho FDs)](/assets/img/2020-01-23-13-08-27.png)
Exercises: based on IR1, IR2, IR3 proof correctness of rules IR4, IR5, IR6  
missing...  
## Equivalence of Sets of FDs
missing...
## Minimal Sets of FDs
missing...
# Normal form based on Primary Keys
## Normalization of Relations:
* The process of **decomposing** _unsatisfactory "bad" relations_ by **breaking** up their _attributes_ **into** _smaller relations_  
* **Normal form:** **condition** using **keys** and **FDs** of a relation to **certify** _whether_ a relation schema _is in a particular normal form_  
* 2NF, 3NF, BCNF
    * **based on FDs** of a relation schema
    * Additional properties may be needed to ensure a good relational design (lossless join, dependency preservation)
* 4NF
    * **based on multi-valued** dependencies : MVDs;
* 5NF
    * **based on join** dependencies : JDs

## [Practical Use of Normal Forms](/assets/img/2020-01-23-13-37-17.png)
## [Definitions of Keys and Attributes Participating in Keys](/assets/img/2020-01-23-13-38-31.png)
## [First Normal Form](/assets/img/2020-01-23-13-40-27.png)
## [Second Normal Form](/assets/img/2020-01-23-13-41-29.png)
## [Third Normal Form](/assets/img/2020-01-23-13-42-49.png)
## Normal forms defined informally

* 1NF: All attributes depend on the key
* 2NF: All attributes depend on the whole key
* 3NF: All attributes depend on nothing but the key


## [SUMMARY OF NORMAL FORMS based on Primary Keys](/assets/img/2020-01-23-13-47-25.png)

# General Normal Form Definitions (For Multiple Keys)
[def 1](/assets/img/2020-01-23-13-52-47.png)  
[def 2](/assets/img/2020-01-23-13-53-19.png)
[Successive Normalization of LOTS into 2NF and 3NF](/assets/img/2020-01-23-13-55-01.png)

# BCNF (Boyce-Codd Normal Form)
[def](/assets/img/2020-01-23-13-56-21.png)  
[example 1](/assets/img/2020-01-23-13-56-50.png)  
[example 2](/assets/img/2020-01-23-13-57-12.png)  
## Achieving the BCNF by Decomposition
[image 1](/assets/img/2020-01-23-13-57-32.png)  
[image 2](/assets/img/2020-01-23-13-57-50.png)
# Chapter summary
![](/assets/img/2020-01-23-14-00-07.png)