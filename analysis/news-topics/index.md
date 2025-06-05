---
layout: default
title: Headline Topics
date: 2025-06-05
---

## Overview

This project analyzes the latest headlines to surface common themes. The notebook that generates these results runs in three steps:

1. **Load and deduplicate headlines**
2. **Calculate word scores**
3. **Rank the headlines**

Each section below explains the step and presents its current output as an interactive table.

### 1. Load and deduplicate headlines

All stories are pulled from our [headlines collection](../headlines/), ordered by publication date and stripped of duplicate titles.

<div id="step1-table"></div>

### 2. Calculate word scores

The headline text is tokenized and every unique word counted, ignoring the stop words listed in `exclude.txt`. The raw frequency of each word becomes its score.

<div id="step2-table"></div>

### 3. Rank the headlines

For each headline we sum the scores of the words it contains and sort the list from highest to lowest.

<div id="step3-table"></div>

<script>
function loadCsvTable(sel, csvPath){
  fetch(csvPath)
    .then(r => r.text())
    .then(text => {
      const rows = csvToObjects(text);
      const table = ArrTabler(rows);
      $(sel).html(table);
      new DataTable(sel + ' table', {
        order: [[0, 'desc']],
        columnDefs: [
          { targets: '_all', className: 'dt-head-left dt-body-left' }
        ]
      });
    })
    .catch(() => {
      $(sel).text('Unable to load data.');
    });
}

document.addEventListener('DOMContentLoaded', function(){
  loadCsvTable('#step1-table', '../headlines/latest.csv');
  loadCsvTable('#step2-table', './scores.csv');
  loadCsvTable('#step3-table', './rank.csv');
});
</script>

## File Versions:
{% assign csv_files = site.static_files | where:"extname", ".csv" | where_exp:"f","f.path contains 'analysis/news-topics/'" | sort: 'name' | reverse %}
<ol>
  {% for file in csv_files %}
    {% unless file.name == 'latest.csv' %}
  <li><a href="./{{ file.name }}">{{ file.name }}</a></li>
    {% endunless %}
  {% endfor %}
</ol>
