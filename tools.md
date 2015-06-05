---
layout: page
title: Tools
permalink: /tools/
anchorific: true
---

<nav class='anchorific'></nav>

{% assign groups = site.tools | group_by: "category" | sort: "name" %}

{% for group in groups %}
#{{ group.name }}
    {% for tool in group.items %}
##[{{ tool.name }}][{{ tool.slug }}] [->]({{ tool.project-url }})
{{ tool.content }}
    {%endfor%}
{%endfor%}

<!-- <a href="#top" class="top">Scroll to top</a> -->

{% for tool in site.tools %}
[{{ tool.slug }}]: {{ tool.url }}
{% endfor %}
