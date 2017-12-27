---
layout: default
---
| post name | date|
|:------   -|:----|
{% for post in site.posts %}
| [{{ post.title }}]({{post.url}})  | {{ post.date | date: "%b %d, %Y" }} |
{% endfor %}