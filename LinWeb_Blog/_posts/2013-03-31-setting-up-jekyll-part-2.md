---
title: Setting up Jekyll for Blogging - Part 2
layout: post
tags: jekyll, setup, tutorial, part-2
description: In this tutorial, we'll be creating a template for our Jekyll powered website and eventually create some posts so that we can publish them using our templates.
---
<div class='panel series'>
	<h6>Posts of this series:</h6>
	<ul class='no-bullet'>
		<li><a href="{% post_url 2013-03-30-setting-up-jekyll-part-1 %}">Installing Jekyll</a></li>
		<li><a href="{% post_url 2013-03-31-setting-up-jekyll-part-2 %}">Creating the template</a></li>
		<li><a href="{% post_url 2013-04-04-setting-up-jekyll-part-3 %}">Final Changes</a></li>
	</ul>
</div>
This is the second part of the series. We'll be creating the template from ground up and generating the website with all the necessary things. By the end of this post, we'll have a working website to show off.

<!-- more -->

####Sections:

<ol>
	<li><a href="#commands">Important Commands</a></li>
	<li><a href="#file_structure">File Structure</a></li>
	<li><a href="#template_creation">Create the Basic Template</a></li>
	<li><a href="#divide_and_rule">Divide and Rule</a></li>
	<li><a href="#creating_pages_and_posts">Creating Pages</a></li>
	<li><a href="#post_loops">Post Loops</a></li>
	<li><a href="#pagination">Pagination</a></li>
	<li><a href="#one-final-hack">One Final Hack</a></li>
	<li><a href="#conclusion">Conclusion</a></li>
</ol>

<div class='panel series'>
  <h5>Update</h5>
  <p>The new version of Jekyll uses slightly different commands. I've updated the new commands on the appropriate places.</p>
</div>


Once you are done installing Jekyll on your system, you will need to worry a little about a couple of commands you have to learn to apply in the terminal. Yes! The terminal! The arch enemy of most designers. But if you love the terminal, then welcome to my club! 

<h4><a name="commands">Important Commands:</a></h4>

{% highlight sh %}
jekyll build			#compiles your templates and posts into html files

jekyll build --watch			#automatically builds your static files on updation of posts

jekyll server --watch	#automatically builds your static files and hosts it on a local server, localhost:4000
{% endhighlight %}

That's all the commands you will need for now.


<h4><a name="file_structure">File Structure</a></h4>

Jekyll has a specific file structure you must follow. Even though you'll find that a number of other additions may be done, for the sake of ease, I'll include only the ones we'll be using now, namely, <span class='word_highlight'>\_layouts</span>, <span class='word_highlight'>\_includes</span>, <span class='word_highlight'>\_site</span> and <span class='word_highlight'>\_posts</span>.

<img src="/images/setting-up-jekyll-for-blogging-part-2/file_structure_1.jpg" alt='File Structure'>

Why do we use '\_' in the file and directory names? This isn't some vodoo required by Jekyll. The '\_' is added to every file or directry name you don't want to be added in your website. However the site will be generated from the contents of the '_' prepended files.

You might have noticed a file named <span class='word_highlight'>\_config.yml</span>. This is the configuration file for the website we'll be creating. The content of this <span class='word_highlight'>\_config.yml</span> file is:

{% highlight yaml %}
name: "LinWeb"
description: "This is the offcial blog of LinWeb - the brainchild of Sumit"

url: "http://blog.linweb.tk"

paginate: 10

markdown: rdiscount
permalink: pretty
pygments: true
{% endhighlight %}

This is YAML front matter. I'll explain it in brief.

*	<span class='word_highlight'>name</span>:	This is to be followed by the name of your website. In my case it's LinWeb. This is the title of your site.

*	<span class='word_highlight'>description</span>:	Ever seen the meta description tag? Yes, we'll use this there.

*	<span class='word_highlight'>url</span>:	Self describing. But if it's a subdirectory where you'll be placing your website in, you must make sure, you type the right url where you'll be placing the generated site.

*	<span class='word_highlight'>markdown</span>:	I am using <span class='word_highlight'>RDiscount</span> as the Markdown engine.

*	<span class='word_highlight'>paginate</span>: Usually you won't find hundreds and thousands of posts listed in a single home page. They are divided over multiple pages. This is called pagination. We have set a limit of 10 posts per page.

*	<span class='word_highlight'>permalinks</span>:		If you have used pretty links in wordpress or any other CMS, you'll know what it it. For those who don't, permalinks is short name for permanent links. The various posts you'll be creating will be stored in a structured manner as defined by you in the configuration.

*	<span class='word_highlight'>pygments</span>:	As mentioned in [Part-1]({% post_url 2013-03-30-setting-up-jekyll-part-1 %}), Pygments is a syntax highlighter. I am using it because I'll post code snippets in my posts. You may not. So, there's no reason why you should use it.


This was only a couple of YAML configuration settings, you will need. I have only scratched the surface. You'll find an extensive list at the [wiki of Jekyll](https://github.com/mojombo/jekyll/wiki/Configuration). You can change the entire file structure using custom configuration. However, I like to keep things simple.

<h4><a name="template_creation">Creating the Basic Template</a></h4>

Before we begin, I must mention that the templates in Jekyll rely on [Liquid](http://wiki.github.com/shopify/liquid/liquid-for-designers) tags heavily. Don't worry about learning a whole different language. It's preety easy to use. If you can code in HTML and CSS, then you can use Liquid markups too. 

There are two types of markup in Liquid:

*	Output markup which may or may not resolve to text
	

*	Tag markup which cannot resolve to text


Liquid tags are used with basically the same idea as using a CMS where we create pages with the same template but with different content.

Let's create a HTML file first in the <span class='word_highlight'>\_layouts</span> folder.

I love using the [Foundation](http://foundation.zurb.com) framework for quickly coming up with a responsive design. I'll use the same here. I am hoping you are familiar with SASS. Even if you are not, no worries, I'll post a CSS file for you.

<img src="/images/setting-up-jekyll-for-blogging-part-2/layout.jpg" alt="Setting up SASS for designing the template">

We have created a project inside <span class='word_highlight'>\_layouts</span> folder. We'll move the <span class='word_highlight'>stylesheets</span> and <span class='word_highlight'>javascripts</span>, folders out to the root directory. Why? We already know that all the files and folders in the root directory without the '_' prepended in their names are automatically added to the final build. We definitely want our stylesheets and javascripts folders  to be added. However, we want the <span class='word_highlight'>index.html</span> file to become our template. So, we'll keep it right where it is.

<img src="/images/setting-up-jekyll-for-blogging-part-2/new_structure.jpg" alt="Moving the required directories to root folder">

Now to make sure that the SASS files are compiled to CSS files at the right locations, we'll change the contents of <span class='word_highlight'>config.rb</span> to:

{% highlight ruby %}
require 'zurb-foundation'
http_path = "/"
css_dir = "../stylesheets"
sass_dir = "sass"
images_dir = "../images"
javascripts_dir = "../javascripts"

output_style = :expanded
line_comments = false

{% endhighlight %}


Let us build the basic template. I am using my template for example as that would be the best way for me to explain. However, don't get messed up in the jargon of code. Just follow my lead.


{% highlight html %}
<!DOCTYPE html>
<!--[if IE 8]> 				 <html class="no-js lt-ie9" lang="en"> <![endif]-->
<!--[if gt IE 8]><!--> <html class="no-js" lang="en"> <!--<![endif]-->
<head>
	<meta charset="utf-8" />
  <meta name="viewport" content="width=device-width" />
  <title>LinWeb | {{ page.title }}</title>

  <meta name='robots' content='index, follow' />

  <link href='http://fonts.googleapis.com/css?family=Raleway:600,400' rel='stylesheet' type='text/css'>

  <link rel="stylesheet" href="/fonts/banda/stylesheet.css" />
  <link rel="stylesheet" href="/fonts/icomoon/style.css" />

  <link rel="stylesheet" href="/stylesheets/blog.css" />
  

  <script src="/javascripts/vendor/custom.modernizr.js"></script>

</head>
<body>
    <div class='main_container'>
        <nav class='inactive'>
            <h3>Table of Contents</h3>
            <ul>
                <li><a href="{{ site.url }}">Home</a></li>
                <li><a href="{{ site.url }}/archives">Archives</a></li>
                <li><a href="{{ site.url }}/contact">Contact</a></li>
                <li><a href="{{ site.url }}/special-offers">Special Offers</a></li>
            </ul>
            <div class='nav_footer'>
                <p>Copyright: LinWeb</p>
                <p>Built by: <a href="#">Sumit Sarkar</a></p>
            </div>
        </nav>
        <div class='row content_container'>
            <div class='columns large-12'>
                <div class='menu_icon'>
                    <span>&#xe00e;</span>
                </div>
                <header><h1>LinWeb</h1></header>

                <div class='row'>
                    <div class='columns large-12'>
                    	<!--*****Place your Content Here*******-->
                    </div>
              </div>
            </div>
        </div>

        <footer class='footer'>
        <ul class='social'>
            <li class='facebook'><a href="https://facebook.com">&#xe003;</a></li>
            <li class='twitter'><a href="https://twitter.com">&#xe002;</a></li>
            <li class='mail'><a href="mailto:sumit@linweb.tk">&#xe005;</a></li>
        </ul>
        </footer>
    </div>
    
  <script>
  document.write('<script src=' +
  ('__proto__' in {} ? '/javascripts/vendor/zepto' : '/javascripts/vendor/jquery') +
  '.js><\/script>')
  </script>

  
  <script src="/javascripts/foundation/foundation.js"></script>
  <script src="/javascripts/vendor/fastclick.js"></script>
  
  <script>
    $(document).foundation();
  </script>

  <script type="text/javascript">
    window.addEventListener('load', function() {
        new FastClick(document.body);
    }, false);
    $('.menu_icon').click(function(e){
      $('nav').toggleClass('active');
      $('.content_container').toggleClass('nav_active');
      e.preventDefault();
    });
  </script>

  
</body>
</html>


{% endhighlight %}




Ok! That was a lot of markup! Do you see that comment 'Place your Content Here'? If you do, then that's the place that matters most to us.


Let's focus on that piece:

{% highlight html %}

<!-- markup above -->

 <div class='row'>
    <div class='columns large-12'>
       	<!--*****Place your Content Here*******-->
    </div>
 </div>

<!-- markup below -->

{% endhighlight %}

<h4><a name="divide_and_rule">Divide and Rule</a></h4>

Do you remember that we created a folder named <span class='word_highlight'>\_includes</span>? That is the prime benefactor whenever we are going to create templates. If you have worked with any CMS themes or even PHP, you'll know how we include different markup files to create a template or sometimes various templates.

In other words, suppose you have a main page that shows all the posts. And a post page that includes a Comment section and maybe a sidebar. But those are not included in the main page. The rest of the parts are same. So, do we create two separate templates rewriting the same code? Of course not! We'll reuse the same markup to create separate templates and keep on adding or removing whatever we need or don't need.

Using <span class='word_highlight'>\_includes</span> is simple. I needed a <span class='word_highlight'>&lt;div&gt;</span> for including the comments section. The rest of the parts were same. So, here's how divided my markup into two files: <span class='word_highlight'>header.html</span> and <span class='word_highlight'>footer.html</span>.

For including the comments section in the <span class='word_highlight'>post</span> template, I created another file (even though I could have easily created it from the existing <span class='word_highlight'>footer.html</span>): <span class='word_highlight'>footerpost.html</span>

#####header.html

{% highlight html %}
 {% raw %} 
<!DOCTYPE html>
<!--[if IE 8]> 				 <html class="no-js lt-ie9" lang="en"> <![endif]-->
<!--[if gt IE 8]><!--> <html class="no-js" lang="en"> <!--<![endif]-->
<head>
	<meta charset="utf-8" />
  <meta name="viewport" content="width=device-width" />
  <title>LinWeb | {{ page.title }}</title>

  <meta name='robots' content='index, follow' />

  <link href='http://fonts.googleapis.com/css?family=Raleway:600,400' rel='stylesheet' type='text/css'>

  <link rel="stylesheet" href="/fonts/banda/stylesheet.css" />
  <link rel="stylesheet" href="/fonts/icomoon/style.css" />

  <link rel="stylesheet" href="/stylesheets/blog.css" />
  

  <script src="/javascripts/vendor/custom.modernizr.js"></script>

</head>
<body>
    <div class='main_container'>
        <nav class='inactive'>
            <h3>Table of Contents</h3>
            <ul>
                <li><a href="{{ site.url }}">Home</a></li>
                <li><a href="{{ site.url }}/archives">Archives</a></li>
                <li><a href="{{ site.url }}/contact">Contact</a></li>
                <li><a href="{{ site.url }}/special-offers">Special Offers</a></li>
            </ul>
            <div class='nav_footer'>
                <p>Copyright: LinWeb</p>
                <p>Built by: <a href="#">Sumit Sarkar</a></p>
            </div>
        </nav>
        <div class='row content_container'>
            <div class='columns large-12'>
                <div class='menu_icon'>
                    <span>&#xe00e;</span>
                </div>
                <header><h1>LinWeb</h1></header>

                <div class='row'>
                    <div class='columns large-12'>
 {% endraw %}

{% endhighlight %}


#####footer.html

{% highlight html %}

{% raw %}
                </div>
              </div>
            </div>
        </div>

        <footer class='footer'>
        <ul class='social'>
            <li class='facebook'><a href="https://facebook.com">&#xe003;</a></li>
            <li class='twitter'><a href="https://twitter.com">&#xe002;</a></li>
            <li class='mail'><a href="mailto:sumit@linweb.tk">&#xe005;</a></li>
        </ul>
        </footer>
    </div>
	
	

  <script>
  document.write('<script src=' +
  ('__proto__' in {} ? '/javascripts/vendor/zepto' : '/javascripts/vendor/jquery') +
  '.js><\/script>')
  </script>

  
  <script src="/javascripts/foundation/foundation.js"></script>
  <script src="/javascripts/vendor/fastclick.js"></script>
  
  <script>
    $(document).foundation();
  </script>

  <script type="text/javascript">
    window.addEventListener('load', function() {
        new FastClick(document.body);
    }, false);
    $('.menu_icon').click(function(e){
      $('nav').toggleClass('active');
      $('.content_container').toggleClass('nav_active');
      e.preventDefault();
    });
  </script>

  
</body>
</html>
{% endraw %}
{% endhighlight %}


#####footerpost.html

{% highlight html %}

{% raw %}
                  <div id="disqus_thread"></div>
                  <script type="text/javascript">
                      /* * * CONFIGURATION VARIABLES: EDIT BEFORE PASTING INTO YOUR WEBPAGE * * */
                      var disqus_shortname = '******'; // required: replace example with your forum shortname

                      /* * * DON'T EDIT BELOW THIS LINE * * */
                      (function() {
                          var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
                          dsq.src = '//' + disqus_shortname + '.disqus.com/embed.js';
                          (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
                      })();
                  </script>
                  <noscript>Please enable JavaScript to view the <a href="http://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
                  
                </div>
              </div>
            </div>
        </div>

        <footer class='footer'>
        <ul class='social'>
            <li class='facebook'><a href="https://facebook.com">&#xe003;</a></li>
            <li class='twitter'><a href="https://twitter.com">&#xe002;</a></li>
            <li class='mail'><a href="mailto:sumit@linweb.tk">&#xe005;</a></li>
        </ul>
        </footer>
    </div>
	
	

  <script>
  document.write('<script src=' +
  ('__proto__' in {} ? '/javascripts/vendor/zepto' : '/javascripts/vendor/jquery') +
  '.js><\/script>')
  </script>

  
  <script src="/javascripts/foundation/foundation.js"></script>
  <script src="/javascripts/vendor/fastclick.js"></script>
  
  <script>
    $(document).foundation();
  </script>

  <script type="text/javascript">
    window.addEventListener('load', function() {
        new FastClick(document.body);
    }, false);
    $('.menu_icon').click(function(e){
      $('nav').toggleClass('active');
      $('.content_container').toggleClass('nav_active');
      e.preventDefault();
    });
  </script>

  
</body>
</html>
 {% endraw %}
{% endhighlight %}

Did you notice that I sliced the big file into two right at the point where we were supposed to enter our content (that comment I asked you to focus on) ?

Now we'll save all these files into <span class='word_highlight'>\_includes</span> directory.


Once, we are done with the previous step, we can delete the index.html we created in the <span class='word_highlight'>\_layouts</span> directory. Because we'll create two different templates now.

Let's create two files: <span class='word_highlight'>default.html</span> and <span class='word_highlight'>post.html</span>

We'll use <span class='word_highlight'>default.html</span> for creating pages and <span class='word_highlight'>post.html</span> for creating posts. 

######default.html

{% highlight html %}
 {% raw %} 

{% include header.html %}

{{ content }}

{% include footer.html %}

 {% endraw %}

{% endhighlight %}


######post.html
{% highlight html %}
 {% raw %} 

{% include header.html %}

{{ content }}

{% include footerpost.html %}

{% endraw %}

{% endhighlight %}



<h4><a name="creating_pages_and_posts">Creating Pages and Posts</a></h4>

Now that we have created the templates, we can start creating pages for our website. Let's create a About page first.

{% highlight yaml %}

---
layout: default
title: Contact Me
tags: contact,linweb
description: This is the Contact Page of LinWeb. If you have any queries or requests, contact the admin.
---

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse
cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non
proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

{% endhighlight %}



Save this file as <span class='word_highlight'>about.html</span> in your root directory, so that it is automatically included when Jekyll builds our website.

We can similarly create many other pages.

The main part about the above snippet is <span class='word_highlight'>layout</span>. We created two templates in <span class='word_highlight'>\_layouts</span> directory. One was named <span class='word_highlight'>default.html</span> and the other <span class='word_highlight'>post.html</span>. We used <span class='word_highlight'>default</span> in <span class='word_highlight'>layout</span> in the YAML front matter. So, when Jekyll builds our website, it'll process this file and it's contents and based on the YAML front mater, the <span class='word_highlight'>default.html</span> layout will be used.


By now you can guess how we'll build the posts. 

Yes! Using <span class='word_highlight'>layout: post</span> in the YAML front matter of the posts. However, we'll save the posts not as <span class='word_highlight'>.html</span> files but as <span class='word_highlight'>.md</span> (markdown) files in the <span class='word_highlight'>\_posts</span> directory.

<img src="/images/setting-up-jekyll-for-blogging-part-2/posts.jpg" alt='Saving Posts'>

And one more thing. Save your posts with the name that follows the following format:

<span class='word_highlight'>2013-03-28-my-first-post.md</span>

I won't explain why. Try it on your own and you'll know why.

Hint: Remember the line <span class='word_highlight'>permalinks: pretty</span>

You can however change the way you can save your posts. But you should consult the [wiki](https://github.com/mojombo/jekyll/wiki) first to know how to.


But there's one problem with our home page. Our purpose was to build a blog. However, the main page still doesn't show a list of the posts. For that we need to learn a new concept.

<h4><a name="post_loops">Post Loops</a></h4>

Consider this code snippet:

{% highlight html %}
{% raw %}
{% for post in site.posts limit: 5 %}
    <li><a href="{{ post.url }}">{{ post.title }}</a></li>
{% endfor %}
{% endraw %}
{% endhighlight %}

There's a for loop in the above snippet. It works like any other programming language. Still I'll explain it for you.

The <span class='word_highlight'>for</span> loop goes through all the posts you have in your site, i.e., <span class='word_highlight'>\_posts</span> directory, with a limit of 5 latest posts and creates a <span class='word_highlight'>&lt;li&gt;</span> tag with title of the post inside it and links to the post. SInce this is a loop, it recursively looks for the latest 5 posts till all the posts have been checked.

We'll use the same looping technique to create our home page which shows the list of all the blog posts. The updated home page will be:

#####index.html
{% highlight html %}
{% raw %}
---
title: Home
layout: default
tags: linweb,blog,linux,web,design
---
<div class='blog_excerpts'>
	{% for post in site.posts limit:10 %}
	    <h3 class='post_title'>
	    	<a href="{{ post.url }}">{{ post.title }}</a>
	    </h3>
	    <h6 class='post_date'>{{ post.date |  date: "%d %B %Y"}}</h6>
	{% endfor %}
</div>

{% endraw %}
{% endhighlight %}

Now we are almost done. See the result by running in your terminal:

{% highlight sh %}
jekyll serve --watch
{% endhighlight %}

Browse to <span class='word_highlight'>localhost:4000</span> and you'll be able to see your website.

As you can see, there's a [Disqus](http://disqus.com) comment box at the end of the posts you have created. Notice in the template I've removed the <span class='word_highlight'>disqus_shortname</span>. You must have one of your own to use disqus.

We can see our website is working. But somehow there's still a couple of finetuning jobs to do. Let's get on with it.

<h4><a name="pagination">Pagination</a></h4>

I really didn't know how to make this work. I took help from a tutorial by [Andrew Munsell](http://www.andrewmunsell.com/tutorials/jekyll-by-example/#pagination).

If you have more than 10 posts, you'll notice that the latest 10 posts are listed on the home page and the others are lost in some other dimension! It's because you set <span class='word_highlight'>limit: 10</span> in the loop excerpt above.

To me, this is a problem. We need pagination such that other posts are displayed on the next page, say, <span class='word_highlight'>http://example.com/page/2</span>.

So, we'll use the global variable : <span class='word_highlight'>paginator</span>

Remember we set <span class='word_highlight'>paginator: 10</span> in the <span class='word_highlight'>\_config.yml</span> file. So, all we need to do now is remove the <span class='word_highlight'>limit: 10</span> we used in the snippet above and replace <span class='word_highlight'>site.posts</span> to <span class='word_highlight'>paginator.posts</span>.

Now we need to add the <span class='word_highlight'>/page2</span> directory in our generated website folder. The <span class='word_highlight'>paginator</span> global variable has <span class='word_highlight'>previous_page</span> and <span class='word_highlight'>next_page</span> properties. We can now modify our <span class='word_highlight'>index.html</span> to:


{% highlight html %}
{% raw %}
---
title: Home
layout: default
tags: linweb,blog,linux,web,design
---
<div class='blog_excerpts'>
	{% for post in paginator.posts %}
	    <h3 class='post_title'>
	    	<a href="{{ post.url }}">{{ post.title }}</a>
	    </h3>
	    <h6 class='post_date'>{{ post.date |  date: "%d %B %Y"}}</h6>
	{% endfor %}

	<div class='blog_pagination'>
		<ul class='inline-list'>
	        {% if paginator.previous_page %}
	          {% if paginator.previous_page == 1 %}
	          <li><a href="/">Prev</a></li>
	          {% else %}
	          <li><a href="/page{{ paginator.previous_page }}">Prev</a></li>
	          {% endif %}
	        {% else %}
	        <li><span class="disabled">Prev</span></li>
	        {% endif %}
	        {% if paginator.page == 1 %}
	        <li><span class="active">1</span></li>
	        {% else %}
	        <li><a href="/">1</a></li>
	        {% endif %}
	        {% for count in (2..paginator.total_pages) %}
	          {% if count == paginator.page %}
	          <li><span class="active">{{ count }}</span></li>
	          {% else %}
	          <li><a href="/page{{ count }}">{{ count }}</a></li>
	          {% endif %}
	        {% endfor %}
	        {% if paginator.next_page %}
	        <li><a href="/page{{ paginator.next_page }}">Next</a></li>
	        {% else %}
	        <li><span class="disabled">Next</span></li>
	        {% endif %}
	      </ul>
	</div>
</div>
{% endraw %}
{% endhighlight %}



<h4><a name="one-final-hack">One Final Hack</a></h4>

I have to share this! Because I had quite a bit of trouble to solve this. You'll notice that all your posts are fully printed in the main page. Now some people may like it but as far as I know, most prefer the <span class='word_highlight'>Read More</span> link after an excerpt.

Liquid markup makes this possible. All you have to do is change your <span class='word_highlight'>index.html</span> to the following. Do notice the change I made.

{% highlight html %}
{% raw %}
---
title: Home
layout: default
tags: linweb,blog,linux,web,design
---
<div class='blog_excerpts'>
	{% for post in paginator.posts %}
	    <h3 class='post_title'>
	    	<a href="{{ post.url }}">{{ post.title }}</a>
	    </h3>
	    <h6 class='post_date'>{{ post.date |  date: "%d %B %Y"}}</h6>
	    <div class='post_excerpt'>{{ post.content | split: '<!-- more -->' | first }}
	    	<a href="{{ post.url }}">Read More...</a>
	    </div>
	{% endfor %}

	<div class='blog_pagination'>
		<ul class='inline-list'>
	        {% if paginator.previous_page %}
	          {% if paginator.previous_page == 1 %}
	          <li><a href="/">Prev</a></li>
	          {% else %}
	          <li><a href="/page{{ paginator.previous_page }}">Prev</a></li>
	          {% endif %}
	        {% else %}
	        <li><span class="disabled">Prev</span></li>
	        {% endif %}
	        {% if paginator.page == 1 %}
	        <li><span class="active">1</span></li>
	        {% else %}
	        <li><a href="/">1</a></li>
	        {% endif %}
	        {% for count in (2..paginator.total_pages) %}
	          {% if count == paginator.page %}
	          <li><span class="active">{{ count }}</span></li>
	          {% else %}
	          <li><a href="/page{{ count }}">{{ count }}</a></li>
	          {% endif %}
	        {% endfor %}
	        {% if paginator.next_page %}
	        <li><a href="/page{{ paginator.next_page }}">Next</a></li>
	        {% else %}
	        <li><span class="disabled">Next</span></li>
	        {% endif %}
	      </ul>
	</div>
</div>
{% endraw %}
{% endhighlight %}


<h4><a name="conclusion">Conclusion</a></h4>

We have successfully created a template for ourselves. Even though I haven't mentioned styling anywhere, it is an important part. Nobody will like your blog if it's plain ugly. So, I would suggest that you use the concepts you learned in this post or from elsewhere to build your own template from scratch.

Even though we have build the website, there's still a lot to cover. In next post, I'll be covering deployment of your newly built blog and customizing your server to make it super fast. I'll also throw in some SEO techniques. And we'll do some nifty little changes to our template.