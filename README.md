# EMS v1.0 — Execution Management System

A single-page, static web app for tracking execution of the Morocco Campaign
(غذاء وعافية). Built as a self-contained React bundle — no build step, no
server, no database.

## What this is

- A pre-built, minified static bundle (`ems-bundle.js`) containing React,
  ReactDOM, Recharts, and Lucide icons, plus the EMS application code.
- A single `index.html` entry point that loads the bundle and Tailwind CSS
  from a CDN.
- 42 seeded execution tasks across 5 phases, with 21 views (Master Task
  Register, Kanban Board, Gantt Timeline, Executive Dashboard, Risk Register,
  Decision Log, and more).

## What this is NOT

- **Not a shared team tool.** Data is stored in the browser's own
  `localStorage`, scoped per browser/device. Two people opening the same
  deployed URL will each see and edit their own separate copy of the data —
  nothing is synced between them.
- **Not connected to any backend, database, or third-party integration.**
  There is no n8n, no Google Sheets, no Telegram, no API calls of any kind
  besides loading the Tailwind CSS CDN script.
- **Not the Claude Artifact version.** The Claude Artifact version of EMS
  (used inside Claude.ai) uses a different, shared storage backend
  (`window.storage`) and is the canonical multi-user version. This
  repository is a personal-use, browser-local export of the same UI and
  logic.

## Repository structure

```
.
├── index.html        Entry point. Loads Tailwind (CDN) and the app bundle.
├── ems-bundle.js      Pre-built bundle: React + ReactDOM + Recharts +
│                      Lucide + the EMS application code, minified.
├── favicon.svg        Small static icon shown in the browser tab.
├── LICENSE            Usage terms for this repository.
├── .gitignore
└── README.md          This file.
```

There is no `src/` folder and no `package.json` in this repository on
purpose: the bundle is already built. This repository is the *output*
artifact, not the build project. See "Rebuilding the bundle" below if you
need to change the application itself.

## Running locally

No install, no server required. Either:

- Open `index.html` directly in a browser (double-click, or `file://` URL), or
- Serve the folder with any static file server, e.g. `npx serve .`

## Deploying to Cloudflare Pages

This repository requires **zero build configuration**:

| Setting | Value |
|---|---|
| Build command | *(leave empty)* |
| Output directory | `/` (repository root) |
| Framework preset | None |

Connect the repository directly in the Cloudflare Pages dashboard
(**Workers & Pages → Create → Pages → Connect to Git**), or upload the two
files (`index.html`, `ems-bundle.js`) directly via **Upload assets** without
connecting Git at all.

## Rebuilding the bundle

This repository does not include the application source or build tooling.
The bundle was produced from a React source file using `esbuild` with a
small entry-point wrapper that falls back to `localStorage` when the
Claude.ai `window.storage` bridge is not present. Rebuilding is out of scope
for this repository; treat `ems-bundle.js` as a versioned release artifact.

## Data & privacy

All task, risk, decision, and log data entered into this app stays in your
browser's local storage on your device. Nothing is transmitted anywhere
except the one-time load of the Tailwind CSS stylesheet from its CDN.
Clearing your browser's site data for this page will permanently delete all
entered data, with no recovery option.

## Version

EMS v1.0 — static export for personal use.
