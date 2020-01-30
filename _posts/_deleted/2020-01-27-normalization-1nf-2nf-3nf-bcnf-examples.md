---
layout: post
title: Normalization - 1NF 2NF 3NF & BCNF Examples
date: 2020-01-27 21:01 +0000
categories: "Database"
toc: true
---
## Story
The inventor of the relational model Edgar Codd proposed the theory of normalization with the introduction of First Normal Form, and he continued to extend theory with Second and Third Normal Form. Later he joined with Raymond F. Boyce to develop the theory of Boyce-Codd Normal Form
However, in most practical applications, normalization achieves its best in 3rd Normal Form.
## Normalization 
* is a database design technique which organizes tables in a manner that reduces redundancy and dependency of data.
* it divides larger tables to smaller tables and links them using relationships.
* ![](/assets/img/2020-01-27-22-04-34.png)
### Consider this table:
![](/assets/img/2020-01-27-22-10-33.png)
### First Normal Form Rules
* Each table cell should contain a single value.  
* Each record needs to be unique.  

The above table in 1NF:  
![](/assets/img/2020-01-27-22-12-55.png)
### Bổ trợ 2NF
#### What Is Key?
* **A KEY** is a value used to **identify** a record in a table **uniquely**.  
* **A KEY** could be a **single column or** combination of **multiple columns** 
 
#### Primary Key
**A primary key** is a **single column** value used to **identify** a database record **uniquely**.  

It has following attributes:  
* A primary key is **not-NULL**  
* A primary key **value** must be **unique**  
* The primary key values should **rarely** be **changed**  
* The primary key **must be given** a value **when a new record is inserted**.  

#### What is Composite Key?
`A composite key is `**`composed of multiple columns`** `used to` **`identify `**`a record `**` uniquely`**   
In our database, we have two people with the same name _Robert Phil_, but they live in different places. Hence, we require both _Full Name_ and _Address_ to identify a record uniquely. That is a composite key.
![](/assets/img/2020-01-27-22-24-41.png)  

### Second Normal Form Rules

* Rule 1- Be in 1NF
* Rule 2- Single Column Primary Key

To make our simple database in 2NF. We partition the table above to 2 tables: Table 1 contains member information, Table 2 contains information on movies rented.  

![](/assets/img/2020-01-28-00-29-12.png)
**In Table 1**, we have introduced a new column `MEMBERSHIP_ID` which is the _primary key_ for table 1. Records can be uniquely identified in Table 1 using `MEMBERSHIP_ID`  
**In Table 2**, Membership_ID is the [Foreign Key](/assets/img/2020-01-28-00-20-36.png)
![](/assets/img/2020-01-28-00-21-14.png)
#### Why do we need FK?
`For referential integrity.`
-> Now, if somebody tries to insert a value in the `membership_id` field that does not exist in the parent table, an error will be shown!
![](/assets/img/2020-01-28-00-24-26.png)  
The above problem can be overcome by declaring `membership_id`  from **Table 2**  as **foreign key** of `membership_id` from **Table1**  

### Bổ trợ 3NF - Transitive FDs
A transitive functional dependency is when changing a non-key column, might cause any of the other non-key columns to change.  
Consider the table 1. Changing the non-key column Full Name may change Salutation.
![](/assets/img/2020-01-28-00-31-53.png)

### Third Normal Form Rules
* Rule 1- Be in 2NF
* Rule 2- Has no transitive functional dependencies  

To move our 2NF table into 3NF, We have again divided our tables and created a new table which stores Salutations. 
There are no transitive functional dependencies, and hence our table is in 3NF

In Table 3 Salutation ID is primary key, and in Table 1 Salutation ID is foreign to primary key in Table 3

Now our little example is at a level that cannot further be decomposed to attain higher forms of normalization. In fact, it is already in higher normalization forms. Separate efforts for moving into next levels of normalizing data are normally needed in complex databases.  However, we will be discussing next levels of normalizations in brief in the following.
![](/assets/img/2020-01-28-00-28-24.png)
### Other Normal Forms
#### Boyce-Codd Normal Form (BCNF)
Even when a database is in 3rd Normal Form, still there would be anomalies resulted if it has more than one Candidate Key.

Sometimes is BCNF is also referred as 3.5 Normal Form.

#### 4NF (Fourth Normal Form) Rules

If no database table instance contains two or more, independent and multivalued data describing the relevant entity, then it is in 4th Normal Form.

#### 5NF (Fifth Normal Form) Rules

A table is in 5th Normal Form only if it is in 4NF and it cannot be decomposed into any number of smaller tables without loss of data.

#### 6NF (Sixth Normal Form) Proposed

6th Normal Form is not standardized, yet however, it is being discussed by database experts for some time. Hopefully, we would have a clear & standardized definition for 6th Normal Form in the near future...

That's all to Normalization!!!
