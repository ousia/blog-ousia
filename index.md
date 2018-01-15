---
tab: none
title: Scrapbook
layout: page
---

Here you may find random notes of things I don’t want to forget.

Don’t expect too much from these notes. They may contain information about computers or systems in use.

{% assign default_paths = site.pages | map: "path" %}
{% assign page_paths = site.header_pages | default: default_paths %}

{% if page_paths %}
  {% for path in page_paths %}
    {% assign my_page = site.pages | where: "path", path | first %}
    {% if my_page.tab == "none" %}
        {% if my_page.title != "Nothing" %}
            {% if my_page.path != "index.md" %}
1. [{{ my_page.label | default: my_page.title }}]({{ my_page.url | relative_url }})
            {% endif %}
        {% endif %}
    {% endif %}
  {% endfor %}
{% endif %}

