---
title: Redesign Complete
layout: post
tags: redesign, linweb, using, jekyll
description: The design of LinWeb and the LinWeb Blog is complete. Here, I describe how I came across Jekyll and found it to be the perfect tool for building a blog.
---

After a brief venture with Wordpress, I finally decided that it was enough. Everyday it was the same routine. Removing spam comments, monitoring failed login attempts and clicking through the numerous links in the Administration Panel. It had become way too hectic for me. Or maybe I am just too lazy.

<img src="/images/redesign-complete/jekyll.png">

All this effort to handle a tiny blog wasn't enough. And since, I am not that good at PHP, customizing things according to my needs became pretty tough as a whole. So, I started looking around for alternatives to the mighty Wordpress.

<!-- more -->

#####Discovery 1:
Flat File Based CMS. Yes! I have a soft corner for CMSs. I googled for every Flat File CMS I could find and finally after careful introspection, I decided to go with <a href="http://getsimple.info">Get Simple</a>. 

<img src="/images/redesign-complete/getsimple.png">

Get Simple is pretty easy to setup. They claim it to be a 5 minute setup CMS. And it literally took me less time. I liked it so so much that I even built a theme on my own. It wasn't pretty but it was enough to get the happiness of creating a theme for a CMS for the first time. 

But only after 2 or 3 posts, I got sick of it too. No doubt it's a great CMS. But somehow, the features seemed way too many for my taste. 

So.... the dicovery begins again.

#####Discovery 2:

Static Site Genrators. 

Ah! Generators! Seemed like a shortcut method of getting a good website. If you think so too, you are in it for a disappointment. These do generate a website...alright! But there's a lot of work one must apply to it. There's always a pitfall.

As lazy as I am, in a weird way I was attracted to it. The provision of customizing everything according to my whims was way too tempting for me. So I decided to give it a go.

During my search for some of the best and most frequently updated static site generators, I cam upon the following: 
<ul class='circle'>
	<li><a href="http://github.com/mojombo/jekyll">Jekyll</a> - Ruby Based</li>
	<li><a href="http://github.com/ddfreyne/nanoc">nanoc</a> - Ruby Based</li>
	<li><a href="http://blogofile.com/">Blogofile</a> - Python Based</li>
	<li><a href="http://ringce.com/hyde">Hyde</a> - Python Based</li>
</ul>

And many more...

#####Selection Criteria

Did I mention I am lazy? If I did, then you'll certainly agree with the my selection criteria:
<ul class='circle'>
	<li>Don't force me learn too many languages</li>
	<li>Easily create layouts</li>
	<li>Have extensive documentation</li>
	<li>Great Community Support</li>
	<li>Lots of code available that can be copied</li>
</ul>

And finally <a href="http://github.com/mojombo/jekyll">Jekyll</a> won the trophy! 

Jekyll is not just any static site generator. It's the engine behind <a href="http://pages.github.com/">GitHub Pages</a>. Jelyll is very blog aware. One can easily import blog posts from existing Wordpress, Drupal, Movable Type, TextPattern, Typo, Blogger, Blogspot, Tumblr etc. So, blog migration is extremely easy. Moreover, there's 
<ul class='circle'>
	<li>Pagination</li>
	<li>Permalinks</li>
	<li>Tags</li>
</ul>


Jekyll uses the Liquid Templating Engine to process the templates of the blog. There are numerous extensions available too. So, once the basic template is created, all the author needs to do is write down the posts in <a href="http://daringfireball.net/projects/markdown/">Markdown</a> or <a href="textile.sitemonks.com">Textile</a> whichever seems easy.

I prefer Markdown. I have been using it for a while. So, I decided to stick with it. Moreover I didn't have my previous Wordpress installation and the posts I wrote then. All I had to do was install Ruby on Rails on my system, install the gems of Jekyll and I was good to go!

Now some of the skeptic ones among you might ask, "Why Jekyll? Why leave the comfort of readymade themes and CMS to go for static websites?"

I'll list some of the reasons why

<ul class='circle'>
	<li>You really DO NOT need a full blown CMS with SQL database and PHP for a small blog.</li>
	<li>It's tougher to handle and customize themes of CMSs.</li>
	<li>The requests made to the SQL database everytime a user visits the page is an overhead and hence makes the CMS installation respond slower. Jekyll is fast since it's only static pages. Moreover, if one uses caching, then its SUPER FAST!!</li>
	<li>Jekyll is secure. If you are working on a CMS, you'll realize that you worry a lot about being hacked. Tons of plugins to handle spam and malicious login attempts do make the server slower. With Jekyll, all you have to care about is the security of your server, ie, you root password.</li>
	<li>Jekyll doesn't need any server side languages. All it needs is a webserver. You have a plethora of choices in that regard: Apache, Nginx, Lighttpd, etc. I recommend Nginx with FPM caching.</li>
	<li>Updating of website can be done by uploading the new pages via FTP. No fuss there.</li>
	<li>This is the most important one: If you really can't afford a server or a shared hosting plan. And you donot wish to go to those free hosts since one can't really trust them, you can always use Dropbox. Yes! Dropbox! Even I couldn't believe it the first time.</li>
</ul>

There are many more good things about using Jekyll.

But as I said Jekyll has its pitfalls. If you are not comfortable with using the command line, then Jekyll is not your cup of tea. Installing Ruby on Rails is quite a pain in the butt. It's preinstalled in Mac. But for Windows users it can be a bit tough. I'll leave Linux users out of the loop because I believe you can figure things out yourself. Moreover, if your website depends on user generated data, then Jekyll can't help you. You will need server side languages and database for those. Having multiple authors may cause some trouble too.

But if a simple blog is all you need, then Jekyll will fit right into your lives. Lightweight, fast, secure. Isn't this what everybody needs? 

I'll be posting tutorials on how to setup a Jekyll production server in the upcoming posts soon.