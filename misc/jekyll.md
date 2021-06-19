---
parent: Misc
nav_order: 0
---
# Jekyll

Jekyll is a ultra simple static web site generators which is particularly popular for blogs. It takes in content and configuration and converts them into html/css which can be deployed on static web servers like nginx. Jekyll has a vibrant community with lot of open source themes to choose from. Beloved github pages is powered by Jekyll. Unlike most of the cheat sheets in this site, Jekyll is based on Ruby instead of JavaScript.

Here's how you get started.

```bash
$ gem install jekyll bundler
$ jekyll new myblog
$ cd myblog
$ bundle exec jekyll serve
```

This should install and run the server at `http://127.0.0.1:4000/` with a default theme. You can edit the markdown files to change the content. In the below tutorial, however we will create a site from scratch to understand how this works. [Reference](https://jekyllrb.com/docs/step-by-step/01-setup/).


## Initialize Project

Jekyll works with ruby. `gem` and `bundler` are equivalent of npm from js. Let's initialize empty project:

```bash
$ mkdir jekyll-site
$ cd jekyll-site/
$ bundle init
$ echo 'gem "jekyll"' > Gemfile
```

We'll prefix `bundle exec` to use jekyll from the current directory. Let's create a `index.html`:

```html
<!-- index.html -->
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Home</title>
  </head>
  <body>
    <h1>Hello World!</h1>
  </body>
</html>
```

Run the following in terminal.

```bash
$ bundle exec jekyll build
Configuration file: none
            Source: /Users/sasank/projects/frontend-roadmap/test/jekyll-site
       Destination: /Users/sasank/projects/frontend-roadmap/test/jekyll-site/_site
 Incremental build: disabled. Enable with --incremental
      Generating... 
                    done in 0.006 seconds.
 Auto-regeneration: disabled. Use --watch to enable.
$ ls 
Gemfile		Gemfile.lock	_site		index.html
$ ls _site/
index.html
```

You'll see that `_site` has our built static files. Use serve to update the build and serve as we make changes:

```
$ bundle exec jekyll serve
Configuration file: none
            Source: /Users/sasank/projects/qure/frontend-dev/frontend-roadmap/test/jekyll-site
       Destination: /Users/sasank/projects/qure/frontend-dev/frontend-roadmap/test/jekyll-site/_site
 Incremental build: disabled. Enable with --incremental
      Generating... 
                    done in 0.005 seconds.
 Auto-regeneration: enabled for '/Users/sasank/projects/qure/frontend-dev/frontend-roadmap/test/jekyll-site'
    Server address: http://127.0.0.1:4000
  Server running... press ctrl-c to stop.

```

## Liquid templates

But so far we've not done much. Let's start doing cooler stuff with [liquid template engine](https://shopify.github.io/liquid/basics/introduction/). Template engine is kind of like React components but dumber with its own scripting language. Here are ultra basics:

* Objects: ``{{variable}}``
* Logic: ``{% if page.show_sidebar %} My side bar {% endif %}``
* Filters (or functions): ``{{ "hi" | capitalize }}``

We'll pick this up on the go. Let's add liquid to our index.html

```html
<!-- index.html -->
---
# these metadata insider --- are called front matter.
# front matter tells Jekyll to process Liquid
# you can also keep metadata that you can access using page object
title: "Welcome to Jekyll"
my_number: 4
---

<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>{{ page.title }}</title>
  </head>
  <body>
    <h1>{{ "Hello World" | downcase }} #{{page.my_number}}</h1>
  </body>
</html>
```

## Layouts

Suppose you want to now have a `about.html` page. Copying paste all the html again is not cool. So we can use layouts to maximize the code reuse. Create a file `_layouts/default.hml`

```html
<!-- _layouts/default.hml -->
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

To use this layout, you've to just add to front matter. `content` will be replaced by content of the file which uses this layout.  So modify index.html to follows:

```
<!-- index.html -->
---
layout: default
title: "Welcome to Jekyll"
my_number: 4
---

<h1>{{ "Hello World" | downcase }} #{{page.my_number}}</h1>
```

Now there's just one place to modify `head` of your html! Now you can build `about.html` very easily. Let's use another trick of Jekyll: it can work with markdown!

```
<!-- about.md -->
---
layout: default
title: "About"
---

# About page

Hi! My name is Sasank.
```

## Includes

Open `http://localhost:4000/about.html` and checkout your new about page :). Let's now add nav bar to the site. Ideal place to add that is `_layouts/default.html`. But we'll learn includes and use that in the default layout. Add this to `_includes/navigation.html`

```
<!-- _includes/navigation.html -->
<nav>
  <a href="/">Home</a>
  <a href="/about.html">About</a>
</nav>
```

Now modify `_layouts/default.html`

```
<!-- _layouts/default.html -->
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

That's it, you now have a navigation bar! Ok that's cool where do I keep css, images and other assets? Well, you can keep anywhere but it's recommended to keep them in `assets` folder.

## Content

Jekyll doesn't need or support any database. So where does actual content live? On file system inside `_posts` directory. Let's create two posts: one in markdown and other in html.

```markdown
<!-- _posts/2018-08-20-bananas.md -->
---
title: Bananas
layout: post
author: jill
---
A banana is an *edible* fruit – botanically a berry – produced by several kinds
of large herbaceous flowering plants in the genus Musa.
```

and 

```html
<!-- _posts/2018-08-21-apples.html -->
---
title: Apples
layout: post
author: jill
---

<h2>Apples are awesome</h2>

Apple is a <em>sweet</em>, edible fruit produced by an apple tree.
```

Note that we've used a different layout `post`. So let's create a `_layouts/post.html`

```html
<!-- _layouts/post.html -->
---
layout: default
---
<h1>{{ page.title }}</h1>
<p>{{ page.date | date_to_string }} - {{ page.author }}</p>

{{ content }}
```

Note the inheritance of layouts. You should be now able to open `http://localhost:4000/2018/08/21/apples.html`. This is cool, but how do I list all my posts in my home page? Liquid comes to your rescue. Edit index.html:

```html
<!-- index.html -->
---
layout: default
title: "Welcome to Jekyll"
my_number: 4
---

<h1>Latest Posts</h1>

<ul>
  {% for post in site.posts %}
    <li>
      <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>
```

There are more stuff you can do with jekyll including configuration, data files and so on. But this is all you need to know to understand the basics of jekyll. I recommend picking up one of the [free themes](http://themes.jekyllrc.org/) from here and build your blog!