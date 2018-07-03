---
# Page settings
layout: default
keywords:
comments: false

# Hero section
title: MN United FC!
description: 


# Micro navigation
micro_nav: true

# Page navigation
page_nav:
    prev:
        content: "/"
        url: '/'
    next:
        content:
        url: 

# disqus
comments: false
---
<div class="content"> 

<h3>Posts: {{site.posts | size}}</h3>

{% for post in site.posts %}

		<div>
			<h1><a href="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}{{ post.url }}">{{ post.title }}</a></h1>
			<p class="date">{{ post.date | date: "%b %d, %Y" }}</p>
		</div>
		<div>
            {{ post.excerpt }}
            <a href="{{ post.url }}">Read more</a>	
        </div>

	
{% endfor %}
</div>