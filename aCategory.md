---
layout: default
---
{% for category in site.categories %}
	{% if category.first == page.category %}
		{% for post in category.last %}
[{{ post.title }}]({{post.url}}) {{ post.date | date: "%b %d, %Y" }} |
		{% endfor %}
	{% endif %}
{% endfor %}