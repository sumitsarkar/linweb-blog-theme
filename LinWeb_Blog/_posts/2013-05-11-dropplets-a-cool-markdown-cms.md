---
title: Dropplets - A Wicked Cool Markdown CMS
layout: post
tags: dropplets, blog, markdown, cms
description: Bloggers need simplicity. Complex dashboards are a total turnoff for anyone who just wants to write a blog post. Maybe it's time for something simpler.
---

I had been waiting for my exams to get over before I could plunge into the web world to discover or build something exciting. And I cam across [Dropplets](http://dropplets.com). It attracted me, intrigued me!

I know I am quite biased towards databaseless lightweight CMSs. But Dropplets made quite an impression.

Dropplets is a project by [Jason Schuller](http://jason.sc/). Jason is a wonderful Wordpress Theme Developer. In [one of his personal blog posts](http://jason.sc/life-beyond-wordpress), he argues how Wordpress is not the solution to everything. He feels that creativity is being lost due to the availability of readymade full featured themes. And this is the reason he started working on Dropplets.

> Introducing Dropplets, a fresh platform dedicated to making blogging simple again. There's no database or confusing admins to worry about. Install in seconds, compose in markdown, then drag and drop to publish.

All you need is a working web server with PHP engine running on it. Installing it is also very easy. The documents claim it to be a 30 second install, and Dropplets does live up to this claim. 

All you need to do is download the [source from Github](https://github.com/circa75/dropplets), copy it to your web host directory, and you are good to go. However, if it's nginx your Web Host is using, and not Apache, you will need to make a few changes for the pretty links to work.

If you want it in a separate domain, then add the following lines to the configuration:

{% highlight sh %}
	location / {
        index  dropplets/index.php index.html;
        rewrite ^/(.*)$ /dropplets/index.php?filename=$1 last;

        # If the file exists as a static file serve it
        # directly without running all
        # the other rewite tests on it
        if (-f $request_filename) {
            break;
        }

        if (!-f $request_filename) {
            break;
        }
    }

    location /post {
        index index.php;
    }
    location /dashboard {
        index index.php;
    }
{% endhighlight %}

And if it's a subdirectory, add the following lines to the configuration:

{% highlight sh %}
	location /dropplets {
        rewrite ^/dropplets/(.*)$ /dropplets/index.php?filename=$1 last;

        # If the file exists as a static file serve it
        # directly without running all
        # the other rewite tests on it
        if (-f $request_filename) {
            break;
        }

        if (!-f $request_filename) {
            break;
        }
        }

    location /dropplets/post {
        index index.php;
    }

    location /dropplets/dashboard {
        index index.php;
    }
{% endhighlight %}

Now open up the domain where you installed Dropplets on your browser. And this is what will come up.

![Installation](/images/dropplets-a-cool-markdown-cms/install.jpg)

You'll need to enter your admin email, twitter account, the blog name, a short description of the blog, admin password etc. It's pretty straightforward. Once you are happy with the typed in details, click on the big check button at the bottom of the screen.

And you'll be greeted with the home page of the blog.

![Blog](/images/dropplets-a-cool-markdown-cms/blog.jpg)

The dashboard can be accessed by going to http://your-blog-url/dashboard/

![Dashboard](/images/dropplets-a-cool-markdown-cms/dashboard.jpg)

The dashboard is dead simple to use. There are three buttons on the top. One is to go to the blog homepage, another is for changing the settings, and the last one for changing themes. Dropplets comes with two inbuilt themes. Both are responsive. 

You need to create your blog posts in markdown format offline and just drag and drop them on the huge droplet in the center of the dashboard. Dropplets will automatically add the new posts to the blog.

The settings option lets one inject custom styling and tracking codes. This might come handy if you are using an analytics solution.

Even though proper documentation for building custom themes is yet not available, it'll be soon. Till then you can read the source and try to build one on your own.

Dropplets is a breeze to use and it's lightweight nature will definitely attract users who just want a self-hosted blog without much hassle.

