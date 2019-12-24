---
layout: post
title: Jekyll Notes
date: 2019-12-18:+0100
ordered: true
---
{% raw %}
## Build

We need Jekyll to build the site before we can view it:

* `jekyll build` - Builds the site and outputs a static site to a directory called `_site`.
* `jekyll serve` - Does the same thing except it rebuilds any time you make a change and runs a local web server at `http://localhost:4000`.

## Liquid

Liquid is a templating language which has three main parts: objects, tags and filters.

### Objects:

Objects tell Liquid where to output content. They’re denoted by double curly braces: `{{` and `}}`.

```
{% raw %}
{{ page.title }}
```

Outputs a variable called `page.title` on the page.

### Tags:

Tags create the logic and control flow for templates. They are denoted by curly braces and percent signs: `{%` and `%}`. For example:

```
{% if page.show_sidebar %}
  <div class="sidebar">
    sidebar content
  </div>
{% endif %}
```

Outputs the sidebar if `page.show_sidebar` is true.

### Filters:

Filters change the output of a Liquid object. They are used within an output and are separated by a `|`. For example:

```
{{ "hi" | capitalize }}
```

Outputs `Hi`. 

## Front Matter

Front matter is used to set variables for the page. It sits between two triple-dashed lines at the top of a file. For example:

```
---
my_number: 5
---
```

Front matter variables are available in Liquid under the `page` variable. For example to output the variable above you would use:

```
{{ page.my_number }}
```

**Use front matter**. Let’s change the `<title>` on your site to populate using front matter:

```
---
title: Home
---
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>{{ page.title }}</title>
  </head>
  <body>
    <h1>{{ "Hello World!" | downcase }}</h1>
  </body>
</html>
```

## Layouts - Bố cục:

Layouts live in a directory called `_layouts`
To have `index.html` use layout `default`, set a `layout` variable in **front matter**. The layout will wrap around the content of the page `index.html`.

```
---
layout: default
title: Home
---
<h1>{{ "Hello World!" | downcase }}</h1>
```

Create your `default` layout at `_layouts/default.html` with the following content:

```
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>{{ page.title }}</title>
  </head>
  <body>
    {{ content }}
  </body>
</html>
```

There’s **no front matter** and the content of the page is replaced with a `content` variable. `content` is a special variable which is replaced by content of `index.html`.

## Includes:

The `include` tag allows you to **include content from another file** stored in an `_includes` folder.
Create a file for the navigation at `_includes/navigation.html` with the following content:

```
<nav>
  <a href="/">Home</a>
  <a href="/about.html">About</a>
</nav>
```

Try using the `include` tag to add the navigation to` _layouts/default.html`:

```
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>{{ page.title }}</title>
  </head>
  <body>
    {% include navigation.html %}
    {{ content }}
  </body>
</html>
```

## Current page highlighting

Jekyll has useful variables available one of which is `page.url`, it returns current page's URL. Edit `_includes/navigation.html`:

```
<nav>
  <a href="/" {% if page.url == "/" %}style="color: red;"{% endif %}>
    Home
  </a>
  <a href="/about.html" {% if page.url == "/about.html" %}style="color: red;"{% endif %}>
    About
  </a>
</nav>
```

## Data Files:

Jekyll supports loading data from YAML, JSON, and CSV files located in a `_data` directory.

### Data file usage

YAML is a format that’s common in the Ruby ecosystem. You’ll use it to store an array of navigation items each with a `name` and `link`.
At _data/navigation.yml, creates:

```
- name: Home
  link: /
- name: About
  link: /about.html
```

Jekyll makes this data file available to you at `site.data.navigation`
Instead of outputting each link in `_includes/navigation.html`, now you can iterate over the data file instead:

```
<nav>
  {% for item in site.data.navigation %}
    <a href="{{ item.link }}" {% if page.url == item.link %}style="color: red;"{% endif %}>
      {{ item.name }}
    </a>
  {% endfor %}
</nav>
```

## Assets:

### Sass

First create a Sass file at /assets/css/styles.scss with the following content:

```
---
---
@import "main";
```

The empty front matter at the top tells Jekyll it needs to process the file. The `@import "main"` tells Sass to look for a file called `main.scss` in the sass directory (`_sass/`).

At this stage you’ll just have a main css file. For larger projects, this is a great way to keep your CSS organized.

Create a Sass file at `/_sass/main.scss` with the following content:

```
.current {
  color: green;
}
```

Edit `_includes/navigation.html` to:

```
<nav>
  {% for item in site.data.navigation %}
    <a href="{{ item.link }}" {% if page.url == item.link %}class="current"{% endif %}>{{ item.name }}</a>
  {% endfor %}
</nav>
```

You’ll need to reference the stylesheet in your layout. Add `<link rel="stylesheet" href="/assets/css/styles.css">` to `<head>` tag of `_layouts/default.html`

## Blogging:

### Posts:

Blog posts live in a folder called `_posts`. The filename for posts have a special format: the publish date, then a title, followed by an extension. Create your first post at `_posts/2018-08-20-bananas.md` with: 

```
---
layout: post
author: jill
---
A banana is an edible fruit – botanically a berry – produced by several kinds
of large herbaceous flowering plants in the genus Musa.

In some countries, bananas used for cooking may be called "plantains",
distinguishing them from dessert bananas. The fruit is variable in size, color,
and firmness, but is usually elongated and curved, with soft flesh rich in
starch covered with a rind, which may be green, yellow, red, purple, or brown
when ripe.
```

### Layout for posts:

Create it at _layouts/post.html with the following content. Notice this is an example of layout inheritance (from layout `default`):

```
---
layout: default
---
<h1>{{ page.title }}</h1>
<p>{{ page.date | date_to_string }} - {{ page.author }}</p>

{{ content }}
```

### List posts:

Jekyll makes posts available at `site.posts`. Create `blog.html` in your root (`/blog.html`) with the following content:

```
---
layout: default
title: Blog
---
<h1>Latest Posts</h1>

<ul>
  {% for post in site.posts %}
    <li>
      <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
      <p>{{ post.excerpt }}</p>
    </li>
  {% endfor %}
</ul>
```

There’s a few things to note with this code:

* `post.url` is automatically set by Jekyll to the output path of the post
* `post.title` is pulled from the post filename and can be overridden by setting `title` in front matter
* `post.excerpt` is the first paragraph of content by default.  

You also need a way to navigate to this page through the main navigation. Open `_data/navigation.yml` and add an entry for the blog page:

```
- name: Home
  link: /
- name: About
  link: /about.html
- name: Blog
  link: /blog.html
```
{% endraw %}