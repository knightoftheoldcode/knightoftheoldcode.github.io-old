---
layout: page
title: About
permalink: /about/
---

## What is Knight of the Old Code?

Knight of the Old Code is the home of Tricorius. 


## Hosting

Knight of the Old Code is hosted on the GitHub Pages platform, powered by Jekyll, a static website generator extraordinaire.

### Versions:

* jekyll: {{ versions.jekyll }}
* kramdown: {{ versions.kramdown }}
* liquid: {{ versions.liquid }}
* maruku: {{ versions.maruku }}
* rdiscount: {{ versions.rdiscount }}
* redcarpet: {{ versions.redcarpet }}
* RedCloth: {{ versions.RedCloth }}
* jemoji: {{ versions.jemoji }}
* jekyll-mentions: {{ versions.jekyll-mentions }}
* jekyll-redirect-from: {{ versions.jekyll-redirect-from }}
* jekyll-redirect-from: {{ versions.jekyll-redirect-from }}
* jekyll-sitemap: {{ versions.jekyll-sitemap }}
* github-pages: {{ versions.github-pages }}
* ruby: {{ versions.ruby }}
        
### Repositories:

{% for repository in site.github.repositories %}
  * [{{ repository.name }}]({{ repository.html_url }})
{% endfor %}
