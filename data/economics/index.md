---
layout: default
title: Economics Data Sources
---

<p><i>Curated economic indicators fetched from the FRED service.</i></p>

## Here are the data sources we collect and curate:

<div markdown="0">

{% assign update_pages = site.pages | sort: "title" %}

{% for page in update_pages %}
  {% assign path_parts = page.path | split: "/" %}
  {% if page.path contains "data/economics/" and path_parts.size == 4 %}
    <hr>
    <p>
      <a href="{{ page.url }}">{{ page.title }}</a><br>
      <small><em>{{ page.date | date: "%B %d, %Y" }}</em></small>
      {% if page.blurb %}<p>{{ page.blurb }}</p>{% endif %}
    </p>
  {% endif %}
{% endfor %}

</div>
