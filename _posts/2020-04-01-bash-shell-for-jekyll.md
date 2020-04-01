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
    
    - Case 2: create errvor - existed
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

# Full code

```bash
#!/bin/sh
cd /Users/steven/Github/yadsendew.github.io
printf "Post title: " && read title
bundle exec jekyll post $title > stdout 2> stderr
if [ -s stderr ] #If error occurs
then
	postname=$(head -1 stderr | cut -d '/' -f 2 | cut -d '.' -f 1)
	postname=$(echo ${postname}.md)
else
	postname=$(tail -1 stdout | cut -d '/' -f 2 | cut -d '.' -f 1)
	postname=$(echo ${postname}.md)
fi
rm stdout > /dev/null
rm stderr > /dev/null
read -r -p "Push? [y/N] " response

if [[ "$response" =~ ^([yY][eE][sS]|[yY])$ ]]
then
	cd _posts
	sed -i '' 's|/Users/steven/Github/yadsendew.github.io/_posts/||g' $postname
	cd /Users/steven/Github/yadsendew.github.io
	path=$(echo _posts/${postname})
	git add $path
	git commit -m "Upload $title"
	git push origin master
fi
```