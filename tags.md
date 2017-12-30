---
layout: default
permalink: "/tags"
---
# tags list
{% for tag in site.tags %}
[{{tag.first}}]({{site.baseurl}}/tag/{{tag.first}})  {{tag.last.size}}
{% endfor %}