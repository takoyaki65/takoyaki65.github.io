---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
---

[About](/about/)

# Posts

{% for post in site.posts %}
  - [{{ post.title }}]({{ post.url | absolute_url }}) ({{ post.date | date: "%B %d, %Y" }}) - {{ post.excerpt }}
{% endfor %}
