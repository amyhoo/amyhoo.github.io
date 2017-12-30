---
layout: default
permalink: "/categories"
---
# categories list
{% for category in site.categories %}
[{{category.first}}]({{site.baseurl}}/{{category.first}})  {{category.last.size}}
{% endfor %}