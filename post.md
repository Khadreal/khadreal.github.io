---
layout: default
title: Blog
permalink: /blog/
---

<ul>
	{% for post in site.posts %}
  		<li>
    		<a href="{{ post.url }}">{{ post.title }}</a>
    		{% assign date_format = site.minima.date_format | default: "%b %-d, %Y" %}
        	<span class="post-meta">{{ post.date | date: date_format }}</span>
  		</li>
	{% endfor %}
</ul>