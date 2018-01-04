---
layout: default
---
# posts
{% for category in site.categories %}
# category: [{{category.first}}]({{site.baseurl}}/category/{{category.first}})  {{category.last.size}}
{% for post in category.last %}
# * [{{ post.title }}]({{post.url}})	{{ post.date | date: "%b %d, %Y" }} 

>tags: {{post.tags | join:' '}}
{% endfor %}
{% endfor %}