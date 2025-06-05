---
layout: default
title: Latest Headlines
date: 2025-06-05
---

## Latest Headlines

A running digest of notable stories from our news feeds.

<div id="headline-table"></div>
<script>
document.addEventListener('DOMContentLoaded', function(){
  HeadlinesLister($('#headline-table'));
});
</script>

## File Versions:
{% assign csv_files = site.static_files | where:"extname", ".csv" | where_exp:"f","f.path contains 'analysis/headlines/'" | sort: 'name' | reverse %}
<ol>
  <li><a href="./latest.csv">Latest version</a></li>
  {% for file in csv_files %}
    {% unless file.name == 'latest.csv' %}
  <li><a href="./{{ file.name }}">{{ file.name }}</a></li>
    {% endunless %}
  {% endfor %}
</ol>
