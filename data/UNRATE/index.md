---
layout: default
title: Civilian Unemployment Rate (monthly)
date: 2025-06-04
---

## Civilian Unemployment Rate (monthly)

<div id="data-table"></div>
<script>
document.addEventListener('DOMContentLoaded', function () {
  const container = document.getElementById('data-table');
  fetch('./latest.json')
    .then(r => r.json())
    .then(d => {
      if (d.observations) {
        arr = d.observations.map(o => ({ date: o.date, value: o.value }));
        table = ArrTabler(arr);
        container.appendChild(table);
        $(table).tablesorter();
      } else {
        container.textContent = 'This source isn't supported for tables yet.';
      }
    })
    .catch(() => {
      container.textContent = 'This source isn't supported for tables yet.';
    });
});
</script>

## File Versions:
1. [Latest version](./latest.json)
2. [2025-06-04.json](./2025-06-04.json)
