---
layout: post
title: Bash shell for Jekyll
date: 2020-04-01 04:00 +0000
---

# Bash shell for Jekyll

Requirements:

- Create new post:
  
  - Read name from user input
  
  - Create new post with given name
  
  - Get name of the post
  
  - Store it to variable

- Wait until user confirm to push
* Push new post to Github: pu.sh
  
  * Get above variable
  
  * Change the path of image inside the post 
    
    ```
    sed -i ''  's|||g' 2020-04-01-bash-shell-for-jekyll.md
    ```

            

![](img/2020-04-01-11-29-01-image.png)



![](img/2020-04-01-11-38-19-image.png)


