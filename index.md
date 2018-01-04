---
layout: default
---
# posts
{% for category in site.categories %}
## *category: [{{category.first}}]({{site.baseurl}}/category/{{category.first}})  {{category.last.size}}
{% for post in category.last %}
>### {{forloop.index}} [{{ post.title }}]({{post.url}})	{{ post.date | date: "%b %d, %Y" }} 

{% assign tagstring="" %}
{% for tag in post.tags %}
{% capture %} 
{{ tagstring | append : [{{tag}}]({{site.baseurl}}/tag/{{tag}})}}
{% endcapture %}
{% endfor %}
>>tags: {{tagstring}}
{% endfor %}
{% endfor %}