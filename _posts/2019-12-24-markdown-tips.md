---
title: Markdown Tips
date: 2019-12-24 20:20:00 Z
layout: post
---

# A collapsible section with markdown
<details>
  <summary>Click to expand!</summary>
  
  ## Heading
  1. A numbered
  2. list
     * With some
     * Sub bullets
</details>
```
<details>
  <summary>Click to expand!</summary>
  
  ## Heading
  1. A numbered
  2. list
     * With some
     * Sub bullets
</details>
```
Make sure **an empty line** sits between `<summary>` and `## Heading`
# Jekyll Drafts & Publish
## Drafts
`bundle exec jekyll draft "Title Of Post`
## Publish
`bundle exec jekyll publish _drafts/title-of-post.md`