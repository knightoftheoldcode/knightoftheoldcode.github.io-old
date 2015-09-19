---
layout: post
title:  "jekyll serve --config"
date:   2015-05-19 06:45:03
description: "jekyll serve --config helps exclude content in development"
categories: article
tags:
- jekyll
---

Very few things anger me more than seeing "localhost" in my Google Analytics code. While there are a few ways to help filter this data out at the server side (which you should probably do anyway) I really just don't like to see "development" data in my production data. (Unlike chocolate and peanut butter, they should remain fully isolated.)

You *could* just comment out certain lines in your `_config.yml` file while developing. But what happens when you forget to uncomment them before a quick push? (It's even *more* irritating to see a huge gap in your analytics than to see "localhost" in there.

:wink:

### Production & development configurations

What would a modern developer do? That's right...flip a table and start their own fork of the project!

However, since those Jekyll folks have thought about nearly everything, fortunately we don't need to do that.

(Note: the "config" flag is suppose to support chaining of yml files so that you can override settings in the main file with settings from latter files in the chain. I've not been super successful with this in practice, so I'm using an alternate method below. I'd prefer the chaining, so I will keep debugging it. If I get it working I'll provide updates to this article.)

#### config.yml

{% highlight yaml linenos %}
# Site settings
title: Knight of the Old Code
email: tricorius@knightoftheoldcode.com
description: > # this means to ignore newlines until "baseurl:"
  Tricorius is the author of a few books and an incredibly popular (in his own mind)
  developer blog. He works on mind-numbingly huge legacy applications to put steak on
  the table while his side-gigs recently added salt and pepper shakers.
baseurl: "" # the subpath of your site, e.g. /blog/
url: "http://knightoftheoldcode.com" # the base hostname & protocol for your site
github_username:  tricorius

google_analytics: UA-62767058-1

# Build settings
markdown: kramdown

permalink: pretty

collections:
  books:
    output: true
    permalink: /books/:path/

gems:
- jekyll-mentions
- jemoji
- jekyll-redirect-from
- jekyll-sitemap
{% endhighlight %}

Above is a faily standard `config.yml` file for Jekyll. You'll notice in line 12 I have a setting defined for a `google_analytics` "UA" code. This works in tandem with my `analytics.html` include.

{% highlight html %}
{% raw %}
{% if site.google_analytics %}
<!-- Google Analytics: change site.google_analytics in _config.yml to be your site's ID. -->
<script>
    (function(b,o,i,l,e,r){b.GoogleAnalyticsObject=l;b[l]||(b[l]=
    function(){(b[l].q=b[l].q||[]).push(arguments)});b[l].l=+new Date;
    e=o.createElement(i);r=o.getElementsByTagName(i)[0];
    e.src='//www.google-analytics.com/analytics.js';
    r.parentNode.insertBefore(e,r)}(window,document,'script','ga'));
    ga('create','{{ site.google_analytics }}');ga('send','pageview');
</script>
{% endif %}
{% endraw %}
{% endhighlight %}

This "if variable present, then include the following code" template is very powerful when creating a forkable repository used to quickly get a new project up to speed. However it can also be extremely useful for implementing a development workflow to exclude the analytics code in a development environment.

You can see by reading the above code (and commenting out line 12 in the `_config.yml` -- if you want to play with this, please feel free to [fork](https://github.com/knightoftheoldcode/knightoftheoldcode.github.io) my code and try it locally) that the analytics block won't be written to the site if the `site.google_analytics` variable is unset.

#### _config-dev.yml

{% highlight yaml linenos %}
# Site settings
title: Knight of the Old Code
email: tricorius@knightoftheoldcode.com
description: > # this means to ignore newlines until "baseurl:"
  Tricorius is the author of a few books and an incredibly popular (in his own mind)
  developer blog. He works on mind-numbingly huge legacy applications to put steak on
  the table while his side-gigs recently added salt and pepper shakers.
baseurl: "" # the subpath of your site, e.g. /blog/
url: "http://knightoftheoldcode.com" # the base hostname & protocol for your site
github_username:  tricorius

# disabled for dev
# google_analytics: UA-62767058-1

# Build settings
markdown: kramdown

permalink: pretty

collections:
  books:
    output: true
    permalink: /books/:path/

gems:
- jekyll-mentions
- jemoji
- jekyll-redirect-from
- jekyll-sitemap
{% endhighlight %}

It's a faily simple matter to duplicate your `_config.yml` file and comment out the analytics line. This will effectively disable the analytics code when jekyll is started with that config file.

Luckily jekyll provides us with options to start the server with an alternate config file chain.

{% highlight bash %}
$ jekyll serve --config _config-dev.yml

Configuration file: _config-dev.yml
            Source: /Users/tricorius/src/knightoftheoldcode/knightoftheoldcode-github-io
       Destination: /Users/tricorius/src/knightoftheoldcode/knightoftheoldcode-github-io/_site
      Generating...
                    done.
 Auto-regeneration: enabled for '/Users/tricorius/src/knightoftheoldcode/knightoftheoldcode-github-io'
Configuration file: _config-dev.yml
    Server address: http://0.0.0.0:4000/
  Server running... press ctrl-c to stop.
{% endhighlight %}

As the console output confirms, we're using the new `_conifig-dev.yml` file. You can further confirm the exlusion of the analytics code in the source code of the generated site.

The trick here, of course, is that you have to remember to launch your local jekyll server with the `_config-dev.yml` configuration file. We'll simplify this in a future article. (Teaser: we'll create a bin directory that holds some scripts. For extra credit, we may just create a Rakefile so you can rake start your jekyll server with your preferred development flags.)