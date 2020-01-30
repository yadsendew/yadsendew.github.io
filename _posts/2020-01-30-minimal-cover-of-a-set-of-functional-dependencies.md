---
layout: post
title: Minimal Cover of a set of Functional Dependencies
date: 2020-01-30 13:01 +0000
categories: "Database"
---
## Definition
![](/assets/img/2020-01-30-14-04-02.png)
## Finding a minimal cover
Call the set `E` is minimal cover of set `F`.  
Initially `E=F` 
* Step 1: **rewrite each FD** that has `m attributes` **on the RHS** into `m FDs` where the **RHS is a single attribute**.

* Step 2: remove trivial FDs.

* Step 3: minimize LHS of each FD  
**For each FD** `X -> y` in `E`, and **for each attribute** `x ∈ X`, if `X – {x} -> y` is implied by `E`, then **replace** `X -> y` with `X - {x} -> y`.

* Step 4: **remove redundant FDs**  
  **For each FD** in `E`, if it is **implied by other FDs** in `E`, then **remove** it from `E`.
## Example 
Suppose:  
```
F = { a,b,c -> c,d,e,f ;
          c -> e       ;
          a -> b       ;
          d -> f       }
``` 
* **Step 1** will rewrite the `a,b,c -> c,d,e,f` into:  
    `a,b,c -> c`  
    `a,b,c -> d`  
    `a,b,c -> e`  
    `a,b,c -> f`  
* **Step 2** will remove `a,b,c -> c`  
    Now:
    ```
    F = { a,b,c -> d   ; 
          a,b,c -> e   ; 
          a,b,c -> f   ; 
              c -> e   ; 
              a -> b   ; 
              d -> f   }
    ```
* **Step 3** will change F to:  
    ```
    F = {   a,c -> d  ; 
              c -> e ; 
            a,c -> f  ; 
              c -> e  ; 
              a -> b  ; 
              d -> f  }
    ```
* **Step 4** will remove `a,b -> f` (since it is implied by `a,c -> d` and `d -> f`), and one of the `c -> e`, and change `F` to the minimal cover.
    ```
    F= { a,c -> d ; 
           c -> e ; 
           a -> b ; 
           d -> f }
    ```