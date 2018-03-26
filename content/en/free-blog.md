---
title: "Build a new blog for free with free SSL certificate."
date: 2018-03-19T21:27:00+09:00
draft: false
slug: free-blog
---

This blog was basically built with [Github page](https://pages.github.com/), but it has some problems.  
Despite you can build your static website in few minutes using Github page, 
it lacks functionality such as TSL/SSL communication and force SSL for that. 
I am using [netlify](https://www.netlify.com/) instead to solve those problems.  

I'm going to explain how you build free SSL blog here.

What you will use are:  
 - [Hugo](https://gohugo.io/)  
 - [Github](https://github.com/)  
 - [Netlify](https://www.netlify.com/)  
 
---
 
![](https://www.kaitoy.xyz/images/hugo-logo.png)

Hugo is one of framework that you can build your article 
and generates static pages on your local environment. This framework is made by Golang, which I love the most.  
It has so [many templates](https://themes.gohugo.io/) and you can easily customize. Why not choosing this framework!
You have other choices if you do not like it. Octopress, 
Hexo and Pelican are also static web site generator, and build your own website. 

To get started, see [this documentation](https://gohugo.io/getting-started/quick-start/) and follow them.

IMPORTANT: The configuration is bit tricky. Need to see examples what you can set for your website.
It depends on templates you chose.
For example see [this page](https://github.com/miguelsimoni/hugo-initio/blob/master/exampleSite/config.toml) 
if you chose [hugo-initio](https://themes.gohugo.io/hugo-initio/) template.


---

![](https://www.netlify.com/img/global/meta-image.jpg)

Netlify allows you to host your web site, with SSL certificate. 
As you see [this issue](https://github.com/isaacs/github/issues/156), you are not able to 
add your SSL certificate to make your site HTTPS with your custom domain.  
Netlify helps you for it.

The easiest way to build your application is to configure with your Github account and setup.  
Build your app, configure your DNS domain and setup SSL, and you can set force SSL 
which force user to use HTTPS access.
You need at least one hour to enable SSL with letencrypt certificate.
  
Now, this blog will generate and show new articles as soon as I push to master branch,
Netlify will build and publish by your source code.

---

#### Conclusion

In this way I show you, knowledge of Git and Markdown are required, however, 
I'm sure this is the cheapest way and easy to setup SSL, including force SSL.     