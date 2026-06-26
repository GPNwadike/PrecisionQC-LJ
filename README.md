# PrecisionQC-LJ

A self-contained, offline clinical laboratory quality control tool implementing
Levey-Jennings charts with static mean, running mean, and Westgard rules.

Built for two goals above all else: **ease of adoption in local or off-network
laboratories**, and **ease of correcting errors or shipping upgrades** later.
Everything here is one HTML file plus a small assets folder — no server, no
build step, no account, no internet connection required.

## Quick start

1. Open `index.html` in any modern browser — no internet required.
2. Demo data for Albumin Level 2 is pre-loaded.
3. Select your analyte, add your runs, set static targets, and analyse.

## Features

- Unlimited analytes and control levels
- Static mean (fixed baseline) vs running mean (rolling average) — switchable
- Real-time drift analysis: running mean vs static mean
- Westgard rules: 1₂ₛ 1₃ₛ 2₂ₛ R₄ₛ 4₁ₛ 10ₓ 7ₜ (individually toggleable)
- Bulk import (comma/newline separated values)
- JSON export/import for backup and transfer between machines
- Corrective action protocol with escalation steps
- Auto-saves in browser localStorage — data persists between sessions
- Visible version marker in the header and browser console, so support
  requests can reference exactly which build is running

## Files

```
PrecisionQC-LJ/
├── index.html                    ← open this in your browser
├── assets/
│   ├── chart.umd.js               ← Chart.js 4.4.1 (bundled, no CDN)
│   ├── tabler-icons.css           ← icon font CSS
│   ├── tabler-icons.woff2
│   └── tabler-icons.ttf
├── README.md
```

## Requirements

- Any modern browser (Chrome, Firefox, Edge, Safari)
- No internet connection needed
- No installation, no Node.js, no server

## Concepts

**Static mean** — the fixed target mean calculated from your 20-day
validation run. This is the center line of the L-J chart and the reference
for all SD limits and Westgard rule checks.

**Running mean** — a continuously updated rolling average of the most recent
N runs. Comparing the running mean against the static mean reveals gradual
systematic drift before individual points breach the ±2SD warning limit.

## Editing and customizing

Everything is editable in a plain text editor (VS Code, Notepad++, or
TextEdit in plain-text mode) — no compiling, no build tools.

- **Colours**: edit the `:root { --bg-primary: ...; }` block near the top of
  `index.html`.
- **Control level names**: edit the `levels:[...]` array in the `<script>`
  block.
- **Analyte list**: edit the `analytes:[...]` array the same way.
- **Operator list as a dropdown** (instead of free text): replace the
  `<input id="en-op">` field with a `<select>` listing your staff initials.

Save the file and refresh the browser tab — changes apply immediately.

## Data backup

Use Setup → Export JSON to save all data. Import the same file on another
machine to restore. Data is also auto-saved in browser localStorage.

## Versioning across deployed copies

The header shows a version string (e.g. `v1.0.0`) and the same string is
logged to the browser console on load. When you edit the code and send an
updated copy to a lab, bump `APP_VERSION` near the top of the `<script>`
block and the version line in the header, so anyone reporting an issue can
tell you exactly which build they're running.
