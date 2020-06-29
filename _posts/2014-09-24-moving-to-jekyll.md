---
title: Moving to Jekyll
excerpt: "Leaving Blogger for Jekyll"
modified: 2014-24-09
tags: [blogger, jekyll, first post]
lang: en
ref: moving-to-jekyll
---

After some time using a very simple google site as landing page and a blogger blog I decided to move everything to [Github pages](https://pages.github.com) + [Jekyll](https://help.github.com/articles/using-jekyll-with-pages).

In my humble opinion under this platform everything looks way more professional. 
To achieve this look a I used [Minimal Mistakes Jekyll theme](http://mademistakes.com/articles/minimal-mistakes-jekyll-theme/).
It comes with very cool fetures such as:

* Minimal design.
* Responsive layouts. Looks good on mobile, tablets, and desktop devices.
* Author sidebar with optional links to social media profiles.
* Disqus comments.
* Google analytics

In order to import all my previous posts from blogger I just used the blogger2jekyll tool, following the steps [here](http://blog.slaks.net/2013-05-31/migrating-from-blogger-to-jekyll)

{% highlight css %}
npm install -g blogger2jekyll
blogger2jekyll  /path/to/blog-dd-mm-yyyy.xml ./_posts
{% endhighlight %}

I had some issues because by default it disabled the comments on the posts, or considered the tags as categories but I didn't have so much posts so I just changed them after manually.

> An important thing for me is that githubpages is for free, also if you use our own domain because I'm not posting everyday and I don't plan to monetize the site,
 I just want a cool landing page and blog.
 
I still need to get used to markdown language, and to "commit" my new posts but hope I can write more often in this platform.



