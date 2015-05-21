---
layout: post
title:  "jekyll bin"
date:   2015-05-20 11:03:11
description: "jekyll bin simplifies setup and other commands"
categories: article
tags:
- jekyll
---

A previous article explained how we can use a jekyll serve flag "--config" to specify a development configuration file. This article continues by creating a useful script to always run "jekyll serve --config" correctly.

{% highlight bash %}
$ mkdir bin
$ touch bin/serve
{% endhighlight %}

The above commands will create a `serve` file in a `bin` directory. The contents of the file are shown below:

{% highlight bash linenos %}
#!/bin/sh

jekyll serve --config _config-dev.yml
{% endhighlight %}

This simply executes the proper jekyll serve command when this script is executed.

{% highlight bash %}
$ ./bin/serve

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

