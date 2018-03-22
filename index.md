---
layout: default
title: Here it is
---

{% for post in site.posts %}

* {{ post.date | date_to_string }} [{{post.title}}](http://{{ site.baseurl }}{{ post.url }})

{% endfor %}
