---
layout: post
title:  "jekyll new . --force"
date:   2015-05-09 02:55:13
description: "jekyll new . --force is the core of my jekyll project generation"
categories: article
tags:
- jekyll
---

I'm a big fan of generators. One of my favorite options in Jekyll is the ability to generate a new site in the current directory and force overwrite it.

I'm a Ruby / Rails developer, so I'm pretty picky with my environment. I prefer rbenv and ruby-build to manage my rubies. Since I use homebrew this is a pretty simple matter. However you don't need to be able to manage multiple rubies to use Jekyll (especially if you're only managing a single site).

The main reason I like "jekyll new . --force" is because it allows me to ensure my environment syncs with GitHub Pages, my preferred deployment method. This is especially helpful in a fully managed ruby environment, but even in a simple setup it is nice to configure your system to use the same versions of Ruby, Jekyll, and supporting libraries that GitHub Pages uses. This helps you ensure that your site appears the same in development and production.

### A new Jekyll project

I prefer to create a "workspace" directory under my user "home" directory. I call mine "src" because I'm a bit old-school. You can pick whatever you want.

I like to create additional directories under this according to the owners of the repositories I use. And then the repository name underneath that (git clone will create this level).

{% highlight bash %}
$ cd ~
$ mkdir src
$ mkdir src/knightoftheoldcode
$ cd src/knightoftheoldcode
{% endhighlight %}

GitHub publishes a gem intended to package up the current versions of the gems used on the GitHub Pages platform. We can take advantage of this by creating the directory for the Jekyll project manually and creating a Gemfile containing the 'github-pages' gem.

We can then use bundler to duplicate the current GitHub Pages environment on our local environment. (Note, it is perfectly safe to skip the 'rbenv local ...' line if rbenv is not configured on your machine. I use it to lock down my local ruby version for the new Jekyll project before I run the bundle installation. One way to find out in advance which ruby you'll need is to check out the [GitHub Pages - Versions][github-pages-versions] page.) 

{% highlight bash %}
$ mkdir knightoftheoldcode-github-io
$ cd knightoftheoldcode-github-io
$ rbenv local 2.1.1
$ echo "source 'https://rubygems.org/'\n\ngem 'github-pages'" > Gemfile
$ bundle install && bundle update
$ jekyll new . --force
{% endhighlight %}

This will configure a default Jekyll project template in your working directory set to keep in sync with GitHub Pages as they update their platform.

A simple ```bundle install && bundle update``` will update your local environment.

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
[github-pages-versions]: https://pages.github.com/versions/
