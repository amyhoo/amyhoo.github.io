---
layout: default
---
# categories list
{% for category in site.categories %}
[{{category.first}}]({{site.baseurl}}/aCategory.html?cat={{category.first}})  {{category.last.size}}
{% endfor %}