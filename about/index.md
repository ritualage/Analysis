# Analysis

This repository hosts data snapshots and Jupyter notebooks for various research
projects published at [analysis.castromedia.org](https://analysis.castromedia.org).
It contains no application code. Instead it tracks raw datasets, the notebooks
that generate results from those datasets, and rendered artefacts that power the
public site.

### Fully narrated workflow (zero code shown)

---

#### 1. Repository structure at a glance

* **`data/`** — holds every raw dataset.
* A single **`catalog.csv`** file lists where each dataset comes from, what file format it uses, how often it should be refreshed, when it was last fetched, and which sub-folder it lives in.
  * Each dataset has its own folder (for example `data/xyz/`). Inside that folder:
    * One file named with the exact download date (such as `2025-06-03.json`) preserves a permanent, timestamped snapshot. The extension matches the catalog's declared file type.
    * A companion file called `latest.json` (or the matching extension) is simply a copy (or symbolic link) to the most recent snapshot, so analyses can always point at a stable filename.
* **`data/update.ipynb`** — the single Jupyter notebook that orchestrates everything: fetching new data, versioning it, and triggering re-analysis.
* **`analysis/`** — contains one sub-directory per research project. Inside each project folder you keep the working notebook, a rendered Markdown version of that notebook, and any static figures (PNG, SVG) the analysis produces.

---

#### 2. How the data-refresh cycle works

1. **Scheduling**
   * The notebook is executed on a separate "dev" machine (your laptop, a lab workstation, or a cheap cloud VM).
   * A local scheduler—cron, Windows Task Scheduler, or an equivalent—starts the notebook at whatever frequency you choose.
2. **Checking the catalog**
   * The notebook opens `catalog.csv`, looks at the "cadence" field for each source (expressed as a standard cron pattern or any other schedule convention you prefer), and decides which datasets are due for an update.
3. **Downloading and versioning**
   * Every dataset that's out of date is downloaded and saved in its folder under today's date.
   * The notebook also refreshes `latest.json` (or whatever extension is specified) so that analyses never need to guess which file is newest.
   * The "last-fetched" timestamp in `catalog.csv` is updated so the next run knows the job is done.
4. **Opening a pull request for data changes**
   * Still within the notebook, a new Git branch is created, the modified files are committed, and a pull request (PR) titled something like "Data refresh – YYYY-MM-DD" is opened on the public repository.
   * Reviewers can inspect every byte that changed before merging.

---

#### 3. How analyses stay in sync

1. **Detecting staleness**
   * After updating any datasets that need it, the same `update.ipynb` notebook scans every analysis notebook in `analysis/`.
   * For each notebook it asks: "Is the newest data file it depends on more recent than the last time this notebook was executed?" This is easy because it will always be a reference to one of the data sources, and we have the list of them because we are still in the updater notebook.
2. **Re-running and publishing**
   * Any notebook deemed stale is executed end-to-end in a headless manner.
   * On completion it produces two kinds of artefacts stored alongside the notebook:
     * A Markdown export of the fresh results, ready for Jekyll to turn into a web page.
     * Static images (plots, diagrams) in PNG or SVG form that the Markdown file references.
     * These images and markdown files are saved as whatever filename, and also as filename_y-m-d so old versions are still viewable on the public website. These should only be saved if they are different from the last saved version. A simple sha comparison is fine.
3. **Opening a pull request for analysis updates**
   * If at least one notebook produced new outputs, the notebook creates a second Git branch, commits the changes inside `analysis/`, and opens another PR (often called "Analysis [NAME] refresh – YYYY-MM-DD").
   * Again, humans can review the exact diff—image hashes, Markdown updates, even regenerated notebooks—before approving.

---

#### 4. What happens after pull requests are merged

Once the two PRs are approved and merged into the main branch:

* GitHub Pages automatically rebuilds the site because Jekyll kicks in on every push to the default branch.
* Visitors immediately see the new tables, text, and figures corresponding to the freshly-acquired data.
* The complete audit trail—datasets, notebook code, and rendered results—lives forever in Git history and in old version files on the public website.

