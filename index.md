---
layout: default
---
# posts

{% for category in site.categories %}
	[{{category.first}}]({{site.baseurl}}/category/{{category.first}})  {{category.last.size}}
	{% for post in site.categories[category] %}
			{% for tag in post.tags %}
				[{{tag.first}}]({{site.baseurl}}/tag/{{tag.first}})  {{tag.last.size}}
			{% endfor %}
	    [{{ post.title }}]({{post.url}})	{{ post.date | date: "%b %d, %Y" }} 
	{% endfor %}
{% endfor %