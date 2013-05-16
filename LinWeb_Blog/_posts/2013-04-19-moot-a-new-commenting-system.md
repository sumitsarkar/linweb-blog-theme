---
title: Moot - A New Commenting System
layout: post
tags: moot, commenting, system
description: A new commenting system just popped up on the internet. But it's not just any commenting system. It has come to revolutionize the present scenario of forums and commenting systems!
---

When it comes to comments, we both love and hate it. Personally I love it. Through this I get to know what I need to work on to get myself better. Well, sometimes, it contains sheer hate too. But I have learnt to ignore them. Anyways, it is pretty damn important for a blogger to have a decent comment system. Fortunately, we already have loads of plugins and 3rd party services for that. If one is using a decent CMS, it'll already have loads of plugins for a comment system. It may be indegenous to the CMS or it maybe  a 3rd party plugin such as [Disqus](http://disqus.com) or [IntenseDebate](http://intensedebate.com) or [LiveFyre](http://livefyre.com) or [Facebook Comment Box](https://developers.facebook.com/docs/reference/plugins/comments/).

There's no doubt that all of these have proved that they are very robust systems. And over time, they have become very social. But 4 days ago, I came across something, which blew my mind away! 

[Moot](http://moot.it) - the new kid in town - is a super cool commenting system which is not only realtime, but also good looking. And if somehow, it doesn't look so good to you, you can easily theme it to your needs. Yes! Custom theming! This is what took my heart away.

<img src="/images/moot-a-new-commenting-system/moot.jpg">

The company was founded by Portland-based serial entrepreneur Courtney Couch, along with jQuery Tools creator Tero Piirainen and Janne Lehtinen, both of Helsinki. The team had previously worked on popular web video player [Flowplayer](http://flowplayer.com). They were not happy with the present support system and forums. They wanted to build a static forum site. Everything they tried looked like from 90s. Well most of the forum software actually does look like that from 90s. This is what led them to build [Moot](http://moot.it).

The vision of Moot is :

<blockquote>Moot is a radically different discussion platform, unencumbered by the weight of unnecessary features and distractions. It places the conversation back to the forefront. Clean user interface, persistent content and deep integration into the site will allow a more natural and meaningful discussion to take place. People will focus on topics they care about.</blockquote>

Moot can not only be used for commenting bul also for creating a full fledged forum. Having a forum is a must for many commercial websites. It helps in providing support to the customers and clients. 

Moot provides a lot of features. It lets one have commenting, forums, flat commenting, threaded commenting. Though adding inline images and videos is not supported out of the box, one can easily add those features because of the configurable nature of Moot.

<img src="/images/moot-a-new-commenting-system/commenting1.jpg">

Site comments can be flat or threaded, but only one level deep to keep threads easier to follow. Comments can be liked by others. The login features login using Facebook or the Moot Login. Admins can manage and remove comments from an online dashboard which is pretty easy to use. Since, it is a real time commenting system, one can expect it to have an online or offline feature available for users. 

To keep the discuassions meaningful, Moot doesn't allow comments to be deleted after a certain time.

<blockquote>Posts or replies on Moot are permanent. Once they are more than 2.7 minutes old, have any replies, or have any likes, they may not be removed.</blockquote>

Moot's core product is free of charge and can be used and embedded by anybody with a valid email address.


Moot is still in beta stage. Upcoming features are:

*	Private Posts
*	Custom Branding
*	Single Sign On

I'll explain a bit on how to implement this in your own blog. All you need to do is paste a couple of lines in your template and be done with it.

Paste the following in your <span class='word_highlight'>&lt;head&gt;</span> tag:

{% highlight html %}

<!-- For mobile responsive look -->
<meta name="viewport" content="width=device-width initial-scale=1.0" />

<!-- Moot look and feel -->
<link rel="stylesheet" href="http://cdn.moot.it/1.1/moot.css"/>

<!-- Moot depends on jQuery v1.7 or greater -->
<script src="http://ajax.googleapis.com/ajax/libs/jquery/1/jquery.min.js"></script>

<!-- Moot client application -->
<script src="http://cdn.moot.it/1.1/moot.min.js"></script>
{% endhighlight %}

Now adding a single line in the <span>&lt;body&gt;</span> will suffice.

{% highlight html %}
<a class="moot" data-label="Your feedback here..." href="http://api.moot.it/your_forum_name/your_path"></a>
{% endhighlight %}


I have only shown how to apply the comment system. You can find details regarding the usage in their [docs](http://moot.it/docs/).

I am so in love with Moot that I decided to ditch [Disqus](http://disqus.com) and move to Moot. Even though I am pretty much using the default styling other than a few minor tweaks, it looks clean on my design.

Time to say goodbye to ugly forums.