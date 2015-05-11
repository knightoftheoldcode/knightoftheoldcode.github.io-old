---
layout: page
title: Books
permalink: /books/
---

{% for book in site.books %}
##[{{ book.title }}: {{ book.subtitle }}][{{ book.slug }}]
{% endfor %}


{% for book in site.books %}
[{{ book.slug }}]: {{ book.url }}
{% endfor %}
