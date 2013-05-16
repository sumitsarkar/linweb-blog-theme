---
title: Setting up Jekyll for Blogging - Part 1
layout: post
tags: jekyll, setup, tutorial, part-1
description: This is the first part of the beginning of the tutorial and here we'll learn how to install Jekyll on our computer.
---

I had promised tutorials regarding setting up of <a href="http://jekyllrb.com">Jekyll</a> last time. Since this is a pretty big task, I have divided this into three parts:

<div class='panel series'>
	<h6>Posts of this series:</h6>
	<ul class='no-bullet'>
		<li><a href="{% post_url 2013-03-30-setting-up-jekyll-part-1 %}">Installing Jekyll</a></li>
		<li><a href="{% post_url 2013-03-31-setting-up-jekyll-part-2 %}">Creating the template</a></li>
		<li><a href="{% post_url 2013-04-04-setting-up-jekyll-part-3 %}">Final Changes</a></li>
	</ul>
</div>

There are various tutorials on how to setup Jekyll for building a static website. However, this one is going to be a bit different. I will be mainly emphasizing on creating a working template in this series. And my development server is a Linux box (Debian based OS). So all the shell commands I type in are tested run on Debain system.

Let's start with it then.

<!-- more -->

Jekyll is Ruby powered. So, first we need to install Ruby on our system. The first thing we need to do is fore up the terminal and type in the following in sh:

{% highlight sh lineos %}
sudo apt-get install ruby1.9.1-dev
{% endhighlight %}

The best way to isntall Jekyll is via RubyGems.

{% highlight sh lineos%}
sudo gem install jekyll
{% endhighlight %}

The above command automatically installs <span class='word_highlight'>directory_watcher</span>, <span class='word_highlight'>liquid</span>, <span class='word_highlight'>maruku</span> and <span class='word_highlight'>classifier</span>.

One may also install <span class='word_highlight'>RDiscount</span> instead of <span class='word_highlight'>Maruku</span> for markdown. For that,

{% highlight sh lineos %}
sudo gem install rdiscount
{% endhighlight %}

You might need code highlighting some day in your blog posts. For that Jekyll has support for a Python based code highlighter - <span class='word_highlight'>Pygments</span>. There are various methods to install <span class='word_highlight'>Pygments</span>. If you prefer <span class='word_highlight'>easy_install</span>,

{% highlight sh lineos %}
sudo easy_install Pygments
{% endhighlight %}

One may also use aptitude for its installation.

{% highlight sh lineos %}
sudo apt-get python-pygments
{% endhighlight %}

And that's it! You have successfully installed Jekyll on your system.