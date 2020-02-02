---
layout: post
title: DB exercise 12 solution
date: 2020-02-02 19:08 +0000
categories: "Database"
---
![](/assets/img/2020-02-02-20-19-26.png)
**Answers:**  
**(a)**  
* `{M}` IS NOT a candidate key since it does not functionally determine attributes `Y` or `P`.  
* `{M, Y}` IS a candidate key since it functionally determines the remaining attributes `P`, `MP`, and `C`.  
    i.e.  
    `{M, Y} -> P`, But `M -> MP`  
    By augmentation `{M, Y} -> MP`  
    Since `MP -> C`, by transitivity `M -> MP`, `MP -> C`, gives `M -> C`  
    By augmentation `{M, Y} -> C`  
    Thus `{M, Y} -> P, MP, C` and `{M, Y}` can be a candidiate key  
* `{M, C}` IS NOT a candidate key since it does not functionally determine attributes `Y` or `P`.  

**(b)**  
REFRIG is not in 2NF, due to the partial dependency `{M, Y} -> MP` (since `{M} -> MP` holds).  
Therefore REFRIG is neither in 3NF nor in BCNF.  
**Alternatively**: BCNF can be directly tested by using all of the given dependencies and finding out if the left hand side of each is a superkey (or if the right hand side is a prime attribute).  
In the two fields in REFRIG: M -> MP and MP -> C. Since neither M nor MP is a superkey, we can conclude that REFRIG is is neither in 3NF nor in BCNF.  
**(c)**  
**LJ1** (lossless join test for binary decompositions): lossless if and only if either:
* `(R1 ∩ R2) -> (R1 - R2)` is in `F+`, or
* `(R1 ∩ R2) -> (R2 - R1)` is in `F+`.
1. `M -> Y, P` is **not existed** in F+
2. `M -> MP, C` is **existed** in F+ => lossless decomposition

![](/assets/img/2020-02-02-20-34-45.png)  


**Answer:**

a.  
* The only candidate key is `{Book_Name, Author, Edition}`. 
* From the example, it would appear that `{Book_Name, Author, Year}` would also be a candidate key **but multiple editions might to appear in a given year**. 

b. 
Yes, we have the following FD: `Book_Name, Edition -> Year`.  
We can decompose to remove this FD in the following way:  
`BOOK (Book_Name, Author, Edition)`  
`BOOK_YEAR (Book_Name, Edition, Year)`  
c.  
Yes, BOOK contains `Book_Name -> Author` and `Book_Name -> Edition`. 

d.  
The final decomposition would look like:  
`BOOK (Book_Name, Edition)`  
`BOOK_AUTHOR (Book_Name, Edition, Author)`  
`BOOK_YEAR (Book_Name, Edition, Year)`
