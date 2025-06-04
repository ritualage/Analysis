---
layout: default
title: Home
---

<h1><a href="https://analysis.castromedia.org">Analysis</a>.<a href="https://castromedia.org">CastroMedia.org</a></h1>

**A platform for primary sociological research based on the latest data from reputable sources on local issues.**


<img src="/assets/images/analysis.gif" class="photo">


## Here are the projects:

<div markdown="0">

{% assign update_pages = site.pages | sort: "date" | reverse %}

{% for page in update_pages %}
  {% assign path_parts = page.path | split: "/" %}
  {% if page.path contains "posts/" and path_parts.size == 3 % and page.path != "posts/index.md" %}
    <hr>
    <p>
      <a href="{{ page.url }}">{{ page.title }}</a><br>
      <small><em>{{ page.date | date: "%B %d, %Y" }}</em></small>
      {% if page.blurb %}<p>{{ page.blurb }}</p>{% endif %}
    </p>
  {% endif %}
{% endfor %}

</div>
