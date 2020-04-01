---
layout: post
title: Bash shell for Jekyll
date: 2020-04-01 04:00 +0000
---

# Bash shell for Jekyll

Requirements:

- Create new post:
  
  - Read name from user input
    `echo 'Post title: ' && read title`
  
  - Create new post with given name
    `bundle exec jekyll post $title`
  
  - Get name of the post:
    
    - Case 1: create success
      `> buff`
      `tail -1 buff | cut -d '/' -f 2`
    
    - Case 2: create error - existed
      `2> buff`
      `head -1 buff | cut -d '/' -f 2`
  
  - Store it to variable:
    
    - Case 1:
      `postname=$(tail -1 buff | cut -d '/' -f 2)`
    
    - Case 2:
      `postname=$(head -1 buff | cut -d '/' -f 2)`

- Wait until user confirm to push
  
  - ```
    echo 'Push? Y/N: '
    read option
    ```
* Change the path of image inside the post 
  
  ```
    sed -i ''  's|||g' $postname
  ```

* Commit & Push new post to Github:

```bash
git add *
git commit -m "Upload $title"
git push origin master
```
