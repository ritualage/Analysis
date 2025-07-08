# Analysis Pipeline

This repository drives [analysis.castromedia.org](https://analysis.castromedia.org), a fully transparent data workflow.

1. **Aggregation** – The `data/` folder stores every raw dataset. A notebook called `update.ipynb` pulls from each source on a schedule, versioning the files and opening a pull request with the changes.
2. **Analysis** – Jupyter notebooks inside `analysis/` use the latest data snapshots to produce figures and markdown reports. When data changes, these notebooks re-run automatically and propose another pull request.
3. **Publication** – Once both pull requests are merged automatically (assuming no conflicts), GitHub Pages rebuilds the site using Jekyll. The rendered HTML lives in this repo so anyone can inspect the exact inputs and outputs.

This setup aggregates data from many sources, analyzes it, and publishes the results in real time. Because every step happens in the open through Git commits and PRs, it offers a maximally transparent workflow for public research.
