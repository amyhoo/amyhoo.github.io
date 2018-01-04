---
layout: default
---
# posts

{% for category in site.categories %}
	[{{category.first}}]({{site.baseurl}}/category/{{category.first}})  {{category.last.size}}
	{% for post in category.last %}
			{% for tag in post.tags %}
				[{{tag}}]({{site.baseurl}}/tag/{{tag}})
			{% endfor %}
	    [{{ post.title }}]({{post.url}})	{{ post.date | date: "%b %d, %Y" }} 
	{% endfor %}
{% endfor %}