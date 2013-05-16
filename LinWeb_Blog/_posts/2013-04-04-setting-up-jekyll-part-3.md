---
title: Setting up Jekyll for Blogging - Part 3
layout: post
tags: jekyll, setup, tutorial, part-3
description: This tutorial describes the different ways that can be employed to deploy a Jekyll powered website. However, I mainly emphasize on the method pertaining to Dropbox for hosting purposes.
---
<div class='panel series'>
	<h6>Posts of this series:</h6>
	<ul class='no-bullet'>
		<li><a href="{% post_url 2013-03-30-setting-up-jekyll-part-1 %}">Installing Jekyll</a></li>
		<li><a href="{% post_url 2013-03-31-setting-up-jekyll-part-2 %}">Creating the template</a></li>
		<li><a href="{% post_url 2013-04-04-setting-up-jekyll-part-3 %}">Final Changes</a></li>
	</ul>
</div>

The third installment of the series deals with the deployment of the Jekyll website we built last time. However I added a little bit about some other static website generators too.

<!-- more -->

####Sections:

<ol>
	<li><a href="#basic">A basic idea</a></li>
	<li><a href="#shared">Shared Hosting</a></li>
	<li><a href="#vps">VPS</a></li>
	<li><a href="#dropbox">Dropbox</a></li>
	<li><a href="#dropboxapps">Dropbox Apps for Jekyll and Beyond</a></li>
	<li><a href="#theend">The End</a></li>
</ol>

<h4><a name="basic">A basic idea about hosting</a></h4>

I feel it'll be really dumb to explain what hosting is. Simply saying, deployment is a way to make available the website to everyone through a proper domain name. Not a proper definition. Still it pretty much explains what we are going to do.

I am mainly going to focus on the free ways to host your website. Not that I don't appreciate having a server, it's just that most people want free stuff. So do I. But I'll mention a couple of ways of hosting the Jekyll powered website which you might already be familiar with.

<h4><a name="shared">Shared Hosting</a></h4>

One of the cheapest ways is to buy a shared hosting plan. However, I have never really come across a shared hosting plan from any reputed company which provides only static file hosting. Since, you won't be needing anything other than FTP and a simple web server, the extra server end parsing and Database server is worthless for you. But if you find one that fits your purpose and your wallet, then go for it!


<h4><a name="vps">Virtual Private Server</a></h4>

Now this is my favorite! I am myself hosting all my websites, including client websites on a VPS. It's like owning a full fledged server but with some usage caps. It might seem like an overkill to some. Configuring a VPS to suit your needs is not the goal of this post. I'll simply state my configuration. You will find several tutorials on the internet regarding the setup procedure. I use nginX with caching for supercharged serving of pages. If that is the only website on your VPS, then I doubt even with quite a bit of traffic, you'll need more than 32MB RAM.

<h4><a name="dropbox">Dropbox</a></h4>

I already mentioned in the first post that one can host the website on Dropbox too. If you google, you'll find a lots of apps that make this easier for you. But, O believe in full control and some of those apps don't give you full control over your website. 

Hosting on Dropbox is extremely easy. But there are some pitfalls. You'll have to use relative links without the '/' ,i.e, root. Normally, in a web server, we can specify the root of a domain or a subdomain. But it's not the case with Dropbox. So, once you have edited all your links, all you have to do is create a directory and copy all the contents of <span class='word_highlight'>\_site</span> directory in your local Jekyll system to that newly created folder.

For domain settings, you'll have to setup a CNAME record in your domain settings and point it to the URL of the <span class="word_highlight">index.html</span> of your website. You can get the URL by sharing that file.

Now all that is to be done is wait for a couple of hours for the DNS to get updated, and the site will be live. However, there are a couple of pitfalls. I am not sure but I've read in a couple of places that sites built this way don't have a good SEO ranking. I am not sure how true that is. If you find the truth behind this and do let me know!

<h4><a name="dropboxapps">Dropbox Apps for Jekyll and Beyond!</a></h4>

I am hoping that you did google for the various techniques of hosting Jekyll websites on Dropbox. And I bet something did come up regarding Dropbox Apps. There are infact a plethora of apps that can make things a lot easier for you. As a matter of fact, you might not need to even create a template! There are apps that provide readymade good looking themes. All you need to do is write posts in markdown. And some of those are not even using Jekyll as their engine. A short list of some of those apps:

<ul class='no-bullet'>
	<li><a href="http://site44.com">site44</a></li>
	<li><a href="http://scriptogr.am">scriptogr.am</a></li>
	<li><a href="http://calepin.co">Calepin</a></li>
	<li><a href="http://skrivr.com">Skrivr</a></li>
</ul>


[site44](http://site44.com) is Jekyll dependent. It has a free plan and even paid plans. They even provide a ".site44.com" subdomain. Password protection is allowed on this domain. However, custom domains do not allow this. However, the bandwidth cap is disappointing. The free plan allows only 100MB/month data transfer. However, if you expect a relatively low traffic, it might suit your purpose. 

[Calepin](http://calepin.co) is a hosted blog that automatically syncs with the Markdown files you store in Dropbox. Pretty much the same as all the apps in the list. However, it's open source. Their codebase is hosted on [Github](https://github.com/jokull/calepin) It is evident from their source that they do not use Jekyll as their engine. 
There are some pitfalls too. They donot allow custom themes. And there's no guarantee that they will remain free forever.


[Skrivr](http://skrivr.com) is quite similar to Calepin. So, I won't describe it further.

[scriptogr.am](http://scriptogr.am) is one app I just fell in love with. Even though they have officially launched on September 05, 2012, their website, still says the app is in beta. But I must say, it's an app beautifully done! Their default theme looks clean and elegant. There are quite a number of themes to choose from. And one has the added advantage of wditing the theme's HTML and CSS. They have opened up their API for developers too. There is provision for submitting apps. 

I have been fiddling with it since this morning. And it's very simple to setup and use. Once you are done clinking on the big orange button <span class="word_highlight">Connect</span> on their home page and allowed the app access to your Dropbox account, you simply have to open up [scriptogr.am](http://scriptogr.am) and edit the posts right from the AJAX powered dashboard. Even the dashboard looks beautiful! Of all the dashboards I've ever seen, their's is the one that took my heart away.

<img src="/images/setting-up-jekyll-for-blogging-part-3/scriptogram_dashboard.jpg">

The CSS and HTML editor are readily available in the <span class="word_highlight">Tools</span> section of the dashboard. And you get a live preview of the changes!

<img src="/images/setting-up-jekyll-for-blogging-part-3/scriptogram_css_editor.jpg">

Adding, editing and delting posts is also very easy. The options are available in the menu.

Finally, the provision for adding custom domain is present in the <span class="word_highlight">Settings</span> page. The following is a modal window that helps in setting up the custom domain.

<img src="/images/setting-up-jekyll-for-blogging-part-3/scriptogram_custom_domain.jpg">

I have setup a live scriptogr.am website for demo purposes.


<a class='flat_button' href="http://scriptogram.linweb.tk/">Demo</a>

<h4><a name="theend">The End</a></h4>

We are done with a static blog creation. I hope all the information will help you in building up a small lightweight blog in avery short time and let that creative beast inside you work on live things without worrying about the languages you don't know. 

Blogging has never been this easier. 
