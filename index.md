---
layout: default
---
{% for category in site.categories %}
- ## :closed_book: [**{{category.first}}**]({{site.baseurl}}/category/{{category.first}})  {{category.last.size}}
{% for post in category.last %}
  - ### :page_with_curl: {{forloop.index}}. [{{ post.title }}]({{post.url}})  <small><small>:bookmark:</small></small> {% for tag in post.tags %} [<small> `{{tag}}` </small>]({{site.baseurl}}/tag/{{tag}}) {% endfor %}      <small>{{ post.date | date: "%Y-%m-%d" }} </small> 

{% endfor %}
{% endfor %}