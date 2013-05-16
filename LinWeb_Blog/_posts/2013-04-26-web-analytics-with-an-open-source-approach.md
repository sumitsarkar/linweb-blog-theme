---
title: Analytics - With an Open Source Approach
layout: post
tags: analytics, piwik, open, source, self, hosted
description: Web Analytics is something which all Website Administrators seek for. However, rarely do we find something which is entirely under our control. Piwik is one tool which changes this situation and gives the reins of web analytics into your very hands.
---

#### What is Web Analytics?

A very trivial matter to explain, however, there may be few who wouldn't know about it. In brief, Web Analytics is a tool which lets a website administrator know who visits his/her website, how many times the visit occurs, which pages get the maximum number of visitors, which keyword searches led to the visitor opening the website, which social network website referred the vistor to get there, how much time a visitor spends on a specific page and so on. 

Web Analytics lets the admin set specific goals too, viz-a-viz, turning the visits into monetary goals, reaching a specific number of visits etc.

####Why we need Web Analytics?

Web Analytics helps an admin to reach goals, see which pages generate most interest, which keywords lead to most hits etc. and in turn she must decide how new content is to be generated so that more vistors are gained. This is very important in today's internet where hundreds of websites dealing with niche topics pop up everyday. So basically there's too much competition to deal with. And only proper tracking of users' interest will help in gaining more visitors and eventually more monetization of the website.

#### What we have in general...

There are a number of Web Analytics service available - both free and paid. The most common ones are:

1. [Google Analytics](http://analytics.google.com)

2. [Clicky](http://clicky.com/)

3. [Mint](http://haveamint.com)

4. [KISSmetrics](http://kissmetrics.com)

5. [Open Web Analytics](http://openwebanalytics.com/)


#### If so many are already available... WHY Piwik?

It is pretty common for people to ask this. But I think Piwik is for the ones whos want full control (Yes. I am a control freak.). I used to be a fan of Google Nalytics, but I moved to Piwik recently. While Google Analytics is no doubt one of the best, if not the best, web analytics services of all time. One doesn't need to worry about servers, upgrades or bacups. All you gotta do is simply login and use it. It has got integrations like social media, advanced graphics like flow reports, in-page analytics, Google Experiments etc.

However, the limitations are rarely highlighted. If ou have ever used it, you must have noticed the analytics are late to show up. The analytics were always shown at least a dozen hours late for me. Moreover, Google Analytics is closed. And there have been repeated complaints regarding tracking the users without their permissions. Moreover, I am not a big fan of companies who track my visitors interests to put up ads at their faces. And I have a soft corner for open source projects. So, I moved to Piwik.

<img src="/images/analytics-an-open-source-approach/piwik.jpg">

Piwik supports almost all the things Google Analytics does right out of the box. And in some ways, it does better.

* All standard statistics reports: top keywords and search engines, websites, top page URLs, page titles, user countries, providers, operating system, browser marketshare, screen resolution, Desktop VS Mobile, engagement (time on site, pages per visit, repeated visits), top campaigns, custom variables, top entry/exit pages,  downloaded files, and many more, classified into four main analytics report categories – Visitors, Actions, Referrers, Goals/Ecommerce (30+ reports)
* Real time data updates - My favorite
* Detailed view of visitors
* Ecommerce support
* Goal Conversion tracking
* Tracking Custom Variables
* World map of visitors
* Automatic file download tracking
* Tracking of 404
* Campaign tracking
* More than 800 Search Engines tracked
* Scheduled email reports
* Embedding reports in app or website


The ones I love most:
* Unlimited users
* Unlimited websites
* Owning all the data
* Paying heed to privacy concerns of visitors
* User privelege
* Options for White Labelling Piwik

Laws in certain places prohibit tracking of user IPs. Piwik has support for anonymising IPs. So privacy concerns are well met.

Integrating Piwik with CMSs is very easy too. There are plugins available for 40+ CMS, web frameworks or Ecommerce shops.

Community support is also great, as expected from Open Source communities.

However, there is a pitfall to using Piwik. Not many people enjoy the agony of hosting, updating and maintaining their own hosted analytics solution. However, if you are one of those who love freedom, then read ahead.

#### How to install Piwik on a server

The minimum requirements are:

* Webserver
* PHP version 5.1.3 or greater
* MYSQL version 4.1 or greater
* PHP extensions pdo and pdo_mysql ot mysqli enabled

More information regarding configuration can be found [here](http://piwik.org/docs/requirements/)

First you need to setup a database for Piwik to use. I recommend creating a separate user for Piwik and give the user permissions over the database.

If you have SSH access to your server, then SSH into it and download the latest Piwik release from [http://builds.piwik.org/latest.zip](http://builds.piwik.org/latest.zip).
Unzip the file and keep the folder <span class='word_highlight'>piwik</span> and delete the rest.

You can upload the folder using FTP as well. 

If you have uploaded the folder to a subdirectory in your domain, then go to: <span class="word_highlight">http://yourdomain.com/piwik</span>.

Now all you have to do is follow the instructions. It'll be a walk in the park. So, I won't explain any further. You should explore yourself.

I have a [hosted Piwik installation](http://analytics.linweb.tk) on my server. I am giving away free logins to interested people. If you want to try out Piwik for your own websites, all you have to do is <a href="mailto:sumit@linweb.tk">mail me</a> with the address of your website and your name.

I'll send you the login once I've reviewed your request.

Do leave a comment below if you have anything more to add. 