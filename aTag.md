--- 
layout: default
---
{% for tag in site.tags %}
	{% if tag.first == page.tag %}
		{% for post in tag.last %}
[{{ post.title }}]({{post.url}}) {{ post.date | date: "%b %d, %Y" }} |
		{% endfor %}
	{% endif %}
{% endfor %}