---
title: "Build a CMS for free"
date: 2018-03-20T20:54:34+09:00
draft: false
slug: netlify-cms
---

As I posted a blog [Build a new blog for free with free SSL certificate.](https://yoshicode.com/en/free-blog/), 
it is easy to build a blog site for free. But it has still disadvantage that need to know Git and markdown.  
So you cannot chose this way to build it if you are building a blog site for non-engineer.

I'm sharing new method to build a CMS (Content Management System) for free with SSL/TLS connection within 30 mins.


## What do we use?

We are going to use those services:
- [Jekyll](https://jekyllrb.com/)  
- [Netlify](https://www.netlify.com/)  
- [Netlify CMS](https://www.netlifycms.org/)


Using Netlify, you will get many pros:
 - Distribute with Netlify CDN
 - Deploy atomatically from GitHub
 - Support HTTP/2
 - Set your custom domain.
 - Support Let's Encrypt


Of course you would get more advantage using wordpress, but is it really so?
It is going to be hassle to setup Database and VPS, upgrading wordpress version and considering security things. 

## Let's get started

**1, Install Jekyll and build a new blog.**
```bash
$ gem install jekyll
$ jekyll new your_blog
```
After building new site, push to Github.


**2, Deploy to Netlify.**

Access to [Netlify](https://app.netlify.com/) and push `New site from Git`.
Select one you deploy just before, and you see those environment settings.

```$xslt
Branch to Deploy: master
Build command: jekyll build
Publish directory: _site
```

And just deploy it. Easy-peacy :D

**3, Custom domain and SSL setting.**

Just setup though Netlify dashboard.

**4, Install Netlify CMS**

You need to create admin folder under path.

```bash
$ touch admin/index.html
$ touch admin/config.yml
```


And edit those files with basic HTML code.
```html
# index.html

<!doctype html>
<html>
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Content Manager</title>

  <!-- Include the styles for the Netlify CMS UI, after your own styles -->
  <link rel="stylesheet" href="https://unpkg.com/netlify-cms@^0.7.0/dist/cms.css" />

</head>
<body>
  <!-- Include the script that builds the page and powers Netlify CMS -->
  <script src="https://unpkg.com/netlify-cms@^0.7.0/dist/cms.js"></script>
</body>
</html>
```

```yaml
# confit.yml

backend:
  name: git-gateway
  branch: master # Branch to update (optional; defaults to master)

publish_mode: editorial_workflow # Editorial Workflow

media_folder: "images/uploads" # Media files will be stored in the repo under images/uploads

collections:
  - name: "post" # Used in routes, e.g. /admin/collections/blog
    label: "Post" # Used in the UI
    folder: "_posts" # The path to the folder where the documents are stored
    create: true # Allow users to create new documents in this collection
    slug: "{{year}}-{{month}}-{{day}}-{{slug}}" # Filename template i.e. YYYY-MM-DD-title.md
    fields: # The fields for each document, usually in front matter
      - {label: "Layout", name: "layout", widget: "hidden", default: "post"}
      - {label: "Title", name: "title", widget: "string"}
      - {label: "Body", name: "body", widget: "markdown"}
```

**5, Setting Identify**

Go `Setting > Identity configuration` and set `Registration preferences` to `Invite only`
And set `External providers` to `GitHub`, and enable `Git Gateway`.

Go `Build & Deploy > Post processing > Snippet injection`
`Add snipet` and insert this code.
```html
<script src="https://identity.netlify.com/v1/netlify-identity-widget.js"></script>
```

## Check if it is working

Open `https://brabra-brabra-123abc.netlify.com/admin/` in your browser.
 
It is all set If you can login and post new posts. 


## To edit your layout

You have [minima](https://github.com/jekyll/minima) template by default to your environment.  
To edit your layouts, you can override it.

[Customization](https://github.com/jekyll/minima#customization) is available.
For example, follow this command to edit post layout.
```bash
$ touch _layouts/page.html
```

```html
---
layout: default
---
<article class="post">

  <header class="post-header">
    <h1 class="post-title">{{ page.title | escape }}</h1>
  </header>

  <div class="post-content">
    {{ content }}
  </div>

</article>
```
this code came from [here](https://github.com/jekyll/minima/blob/master/_layouts/page.html).
Change that code as you want.

more info: https://jekyllrb.com/docs/themes/