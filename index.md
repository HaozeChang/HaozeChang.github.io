---
layout: default
title: Publications
---

{% capture my_markdown_content %}
  {% include_relative publications/publications.md %}
{% endcapture %}


<div>
  {{ my_markdown_content | markdownify }}
</div>

