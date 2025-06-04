---
layout: default
title: Real GDP (chain‑indexed, quarterly)
date: 2025-06-04
---

## Real GDP (chain‑indexed, quarterly)

<div id="data-table"></div>
<script>
document.addEventListener('DOMContentLoaded', function () {
  const container = document.getElementById('data-table');
  fetch('./latest.json')
    .then(r => r.json())
    .then(d => {
      if (d.observations) {
        const arr = d.observations.map(o => ({ date: o.date, value: o.value }));
        const table = ArrTabler(arr);
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
