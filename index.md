---
layout: default
---
# **posts**
{% for category in site.categories %}
- ## :closed_book: [{{category.first}}]({{site.baseurl}}/category/{{category.first}})  {{category.last.size}}
{% for post in category.last %}
  - ### :page_with_curl: {{forloop.index}}. [{{ post.title }}]({{post.url}})  <small>**tags:**</small> {% for tag in post.tags %}[{{tag}} ]({{site.baseurl}}/tag/{{tag}}){% endfor %}  <small>*{{ post.date | date: "%Y-%m-%d" }}* </small> 

{% endfor %}
{% endfor %}