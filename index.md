---
layout: default
---
# **posts**
{% for category in site.categories %}
- ## [{{category.first}}]({{site.baseurl}}/category/{{category.first}})  {{category.last.size}}
{% for post in category.last %}
	- ### {{forloop.index}} [{{ post.title }}]({{post.url}})  <small>**tags:**</small> {% for tag in post.tags %}[{{tag}} ]({{site.baseurl}}/tag/{{tag}}){% endfor %}  <small>*{{ post.date | date: "%b %d, %Y" }}* </small> 

{% endfor %}
{% endfor %}