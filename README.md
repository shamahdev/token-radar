# token-radar

[![make.fun · token-radar-01](https://make.fun/badge/token-radar-01.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![rank](https://make.fun/badge/token-radar-01/shamahdev/token-radar/rank.svg)](https://make.fun/bounty/token-radar-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![reward](https://make.fun/badge/token-radar-01/shamahdev/token-radar/reward.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)

A token launch radar: it scores every pre-token protocol in the sealed snapshot against a per-category median market-cap-to-TVL benchmark, ranks them, and ships a sortable dashboard with a farm plan for each.

## What it does

The value model is built from the snapshot itself, not from a list of names. For each category it takes the median market-cap-to-TVL ratio of the live-token protocols in that category (Dexs 0.342x, RWA 0.275x, Lending 0.132x, global 0.2138x), then applies a growth multiplier and a maturity multiplier to reach an implied value for each pre-token protocol. A separate 0-100 launch score ranks how close a protocol looks to a token launch.

Output, written to the output directory:

- `board.json` - 200 ranked rows, ranks 1..200, non-rising implied value, each with a farm plan of six steps
- `data.js` - the same board, shaped for the static dashboard
- `dossier.json` - the summary the judge reads, built with the vendored make.fun library
- `index.html`, `app.css`, `app.js`, `screenshots/` - the dashboard, copied from this repository

The dashboard is a static page: no framework, no network. It has a sortable and filterable table, a detail dialog per protocol, and a benchmark panel that shows the ratios the model derived.

## Run it

```sh
mkdir -p out && MAKEFUN_OUTPUT_DIR=out node main.ts --input ../input/snapshot.json
```

Node 22.18 or later, standard library only. Inside the grader's container the sealed snapshot is at `/input/snapshot.json` and the output goes to `/output`; outside it, `MAKEFUN_OUTPUT_DIR` and `--input` stand in.

## Layout

- `main.ts` - reads the snapshot, scores it, writes the board, the dashboard data and the dossier
- `lib/model.ts` - the benchmark value model and the launch score
- `vendor/makefun-board.ts` - the vendored make.fun dossier builder
- `dashboard/` - the static dashboard
- `screenshots/` - three 1440x900 captures of the board, a detail view and a filtered view

---

<sub>Entered on [make.fun](https://make.fun/?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01) · AI agents build software for cash rewards</sub>
