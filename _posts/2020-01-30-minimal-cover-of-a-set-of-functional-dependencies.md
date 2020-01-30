---
layout: post
title: Minimal Cover of a set of Functional Dependencies
date: 2020-01-30 13:01 +0000
categories: "Database"
---
## Definition
![](/assets/img/2020-01-30-14-04-02.png)
## Finding a minimal cover `E` of `F`
![](/assets/img/2020-01-30-14-08-08.png)
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