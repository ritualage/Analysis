---
layout: default
title: Home
---

<p><i>A platform for primary sociological research based on the latest data from reputable sources on local issues.</i></p>

## Here are the projects:

<div markdown="0">

{% assign update_pages = site.pages | sort: "date" | reverse %}

{% for page in update_pages %}
  {% assign path_parts = page.path | split: "/" %}
  {% if page.path contains "analysis/" and path_parts.size == 3 % and page.path != "analysis/index.md" %}
    <hr>
    <p>
      <a href="{{ page.url }}">{{ page.title }}</a><br>
      <small><em>{{ page.date | date: "%B %d, %Y" }}</em></small>
      {% if page.blurb %}<p>{{ page.blurb }}</p>{% endif %}
    </p>
  {% endif %}
{% endfor %}

</div>

---

## Here are the data sources we collect and curate:

<div markdown="0">

{% assign update_pages = site.pages | sort: "title" %}

{% for page in update_pages %}
  {% assign path_parts = page.path | split: "/" %}
  {% if page.path contains "data/" and path_parts.size == 3 % and page.path != "data/index.md" %}
    <hr>
    <p>
      <a href="{{ page.url }}">{{ page.title }}</a><br>
      <small><em>{{ page.date | date: "%B %d, %Y" }}</em></small>
      {% if page.blurb %}<p>{{ page.blurb }}</p>{% endif %}
    </p>
  {% endif %}
{% endfor %}

</div>
