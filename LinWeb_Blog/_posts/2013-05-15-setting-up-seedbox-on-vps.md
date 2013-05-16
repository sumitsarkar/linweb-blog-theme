---
title: Setting up Seedbox - The Easy Way
layout: post
tags: seedbox, debian, simple, deluge
description: Even with the stigma attached to torrents, people love it. This is a nifty tutorial to help you set up a seedbox on your low end linux box.
---


I was pissed. I was pissed at the sorry ass speed of the broadband connection I have at home. I was sick and tired of the bottlenecks the ISP had applied on my connection. The speed is an abomination to DSL lines if compared to any first world country. But I can't really complain about it in a third world country. Moreover, I have been noticing really bad speeds (0.1KBps to 4KBps) whenever I am downloading files using torrent (not illegal ones!).

I tried almost every trick in the book to evade the bottlenecks. Nothing seemed to work. I encrypted my data stream, changed the ports, routed the streams to different ports on my router. I even tried to obsfuse the headers of my data streams to fool my ISP. It didn't work. Or maybe I was doing something wrong. Eventually I just laid down my hypothetical arms against this unfair practice of my ISP. 

But last night I was browsing around the web, when it suddenly hit me. . . I can still browse and download at good speeds. So, why can't I download files directly instead of getting bottlenecked by my ISP and wait for a 400MB dile to be downloaded in a week? 

Yes I can!

But how do I get files as direct downloads? There are a couple of websites who allow us to get the files directly instead of getting them through torrents. But almost all of them are spam. So, the only way is to download them using torrent someplace else and then get the downloaded file to my computer with my normal speed.

####All Hail the Seedbox

> Seedbox is a private server used for thr uploading and downloading
> of digital files.
>												-Wikipedia

Think of a seedbox same as your computer downloading files using BitTorrent protocol. The only difference being, it's only job is to download files. Nothing else. And it probably has much much better network connection. Once the downloads are complete, you can simply download the files from the seedbox to your personal computer or smartphone or tablet, whatever you want.

Seedboxes genrally have download and upload speeds of 100Mbit/s (ie. 12.5MB/s). So you can download a 1GB file in about 82 seconds. But since torrent speeds depends on peers, you can't say how much ime it'll take to download. But I bet it'll definitely be faster than your home network connection. 

So, how do we go about it?

First I had to choose a server. The one I am hosting my blog on, allows torrents, game servers and almost anything as long as I do not breach fair usage policy. And it's very fast. Average speed is over 40MByte/s. But I didn't want to screw with a production server. So, I chose an abandoned VPS of mine. I dusted it off by reimaging it first to get a fresh installation (I don't even remember what I had done on it last time I logged into it).

Now I needed something super easy to set up. I use [rtorrent](http://libtorrent.rakshasa.no) on my home computer. But installing gc++, and other libraries and compiling it on a 128MB server without any burst RAM didn't seem a good idea to me. I wanted something much easier. 

####Deluge comes to the rescue

[Deluge](http://deluge-torrent.org/‎) is a standalone torrent client and server that can be setup on Linux systems. I use it frequently on my home computer. And it is also used widely on seedboxes. Therefore, Deluge was the choice I stood out with.

####Setup procedure

Once I had a fresh installation (Debian Squeeze) on the VPS, I ssh'ed into it  and added the dotdeb repository to <span class='word_highlight'>/etc/apt/sources.list</span>.

{% highlight sh %}
echo "deb http://packages.dotdeb.org squeeze all" >> /etc/apt/sources.list
echo "deb-src http://packages.dotdeb.org squeeze all" >> /etc/apt/sources.list
wget -q -O - http://www.dotdeb.org/dotdeb.gpg | apt-key add -
{% endhighlight %}

The I entered the following commands. You may skip them if you want. But it removes most of the stuff you won't need. Ignore the lines starting with <span class='word_highlight'>#</span>. They are just comments to help you know what the command following them does.

{% highlight sh %}
# Update time zone
dpkg-reconfigure tzdata

# Some Debain systems have portmap installed. We don't need it.
apt-get remove portmap

# rsyslogd allocates approximately 30MB on OpenVZ system.
# I couldn't afford losing so much memory on a 128MB server.
apt-get remove rsyslog

# Since I'll be using the lightweight nginx server, I won't need apache
apt-get remove apache2

# There's no need to have a DNS server running
apt-get remove bind9

# Samba is for file sharing on networks. I didn't need it either.
apt-get remove samba

# Sendmail is required for mail servers. Not required for my purpose
apt-get remove sendmail

# Nscd is a daemon that provides a cache for the most common name 
# service requests. 
apt-get remove nscd

# Time to update and upgrade the system
apt-get -q -y update
apt-get -q -y upgrade

# Install dash. Smaller than bash but feature-rich
apt-get install dash
rm -f /bin/sh
ln -s dash /bin/sh

# I prefer nano over vim 
apt-get install nano

# Useful for veiwing running processes
apt-get install htop

# Midnight Commander is a very powerful text based file manager.
# Who knows one day you might need it.
apt-get install mc

# You might not need it. But I do
apt-get install iotop

# To check where all your network speed is going
apt-get install iftop

# Install syslogd. This easts much less memory than rsyslogd
apt-get install inetutils-syslogd

#Let's remove any left out packages not needed anymore
apt-get autoremove

# Let's clean up the apt cache
apt-get autoclean

{% endhighlight %}

Alright! That was quite a lot of installing and removing. Now that I had a optimal system, I needed to install the basic packages for building the seedbox.

As I said before I would be installing Deluge, some might be tempted to just do <span class="word_highlight">apt-get install deluge</span>. DO NOT DO THAT!

This will install a lot of xwindow packages you are not going to need. A seedbox should be headless. I am trying to build a seedbox which is lightweight. This command will install a lot of packages we won't need. So, follow my lead here.

{% highlight sh %}
apt-get install deluge-common deluged deluge-web deluge-console
{% endhighlight %}

<span class='word_highlight'>deluge-common</span> will install the base packages for deluge and <span class='word_highlight'>deluged</span> will install the deluge daemon. 

<span class='word_highlight'>deluge-web</span> is for providing us a nice web based GUI so that we may control it from wherever the hell we want.

<span class='word_highlight'>deluge-console</span> is pretty explanatory itself. It gives us a console based GUI to see what is happening and control deluge configuration from it.

Let's fire up the deluge daemon

{% highlight sh %}
deluged
{% endhighlight %}

Now I had two options. I could either connect to the server using a GTK GUI from my home computer or use the Web based GUI to add torrents. I chose the latter. 

1. **GTK GUI** : 

First you need to add authentication on the server. Use the follwing command:

{% highlight sh %}
echo "username:password:10" >> ~/.config/deluge/auth
{% endhighlight %}

Then you need to configure the server to allow remote connections to it. For that you need to start up the deluge-console.

{% highlight sh %}
deluge-console
{% endhighlight %}

A console based GUI will show up. 

![deluge-console](/images/setting-up-seedbox-on-vps/deluge-console.jpg)

Type in the following to allow remote connections.

{% highlight  sh %}
config -s allow_remote True
{% endhighlight %}

Now, install deluge client on the home system. Start the deluge client and open prefernces. In the Interface tab, *Uncheck Enable Class Mode* and restart the client. 
Now open Connection Manager and enter the server IP, authentication credentials you just used a while ago and leave the port as it is and hit connect. And you are good to go!


2. **Web GUI**

Fire up the deluge-console.

{% highlight sh %}
deluge-console
{% endhighlight %}

Once the console GUI shows up, type in the following command. This command will enable the Web based GUI which we installed while installing deluged and deluge-console.

{% highlight sh %}
plugin -e WebUi
{% endhighlight %}

Now open up a browser and type in your server IP address followed by <span class="word_highlight">:8112</span>, that is, the port address of the WebUi.

example : 66.66.66.66:8112

You'll be greeted with the WebUi. The default password is <span class="word_highlight">deluge</span>. You would want to change the default password. 

![Deluge WebUi](/images/setting-up-seedbox-on-vps/webui.jpg)

The rest of the task is pretty easy. Adding torrents, starting and pausing downloads etc can be done from the Web GUI itself. Just click around a little bit till you get comfortable with the UI. 

####The Important Part

I hope you have downloaded some file by now (hopefully not illegal). Now you need to get it on your computer. For that I used nginx to host the downloaded file. 

Let us install nginx

{% highlight sh %}
apt-get install nginx
{% endhighlight %}

A default configuration file will automatically be created in <span class='word_highlight'>/etc/nginx/sites-available/default</span>. I'll not be using a domain name for this task. So, I'll edit the default configuration file.

We'll edit it to point to the directory where we downloaded the torrent files. Now you might have selected a default download folder in the preferences in the Web GUI. I named it <span class='word_highlight'>torrents</span> and it's in my root directory.

{% highlight sh %}
nano /etc/nginx/sites-available/default
{% endhighlight %}

Contents of default configuration file

{% highlight sh %}
server {
        listen 80;
        root /root/torrents/;
        index index.html index.htm index.php;
        client_max_body_size 32m;

        access_log  /root/access.log;
        error_log  /root/error.log;
}
{% endhighlight %}

Restart the nginx daemon

{% highlight sh %}
/etc/init.d/nginx restart
{% endhighlight %}

That's it! We are setup.

Now when the download is complete, all we need to do is point our download manager to the url of the file. Let's assume the server IP is 66.66.66.66 and the filename is <span class='word_highlight'>abc.pdf</span>.

So, the url of the file will be <span class='word_highlight'>http://66.66.66.66/abc.pdf</span>

![Downloading to home computer](/images/setting-up-seedbox-on-vps/download.jpg)


Now, I have a working seedbox. All I need to take care of is the bandwidth. It can be controlled by limiting the download and upload speed from the WebUi. After all services were running, the memory usage on my VPS was approximately 55MB. 

This is how I evade the torrent restrictions (which I think is there. I am not sure if I am right) from my ISP. Feel free to tell me how you evade torrent restrcitions from your ISP in the comments.