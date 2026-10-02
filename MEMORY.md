# MEMORY.md

Eaton Corporation (NYSE: ETN) tracking dashboard. Static single page served by
GitHub Pages. This repo is independent of `spacex-dashboard`, `tempus-dashboard`,
`nvda-dashboard`, `micron-dashboard`, and `lam-research-dashboard`; keep them
separate (own quote.json, own workflow, own public link).

## Deployment
- Public link: https://tonytcfu.github.io/eaton-dashboard/
- Source: `index.html` at the `main` branch root, generated from the
  `etn-dashboard` web artifact (re-export on data updates; do not hand-edit).
- GitHub Pages setting: Deploy from a branch / main / /(root).

## Quote snapshot
- `quote.json` at repo root; refreshed by `.github/workflows/quote.yml`
  (cron `*/15 13-21 * * 1-5` UTC, Mon-Fri, plus manual dispatch).
- Source: Nasdaq official API (`api.nasdaq.com/api/quote/ETN/info`), real-time.
- Page fallback chain: quote.json -> Nasdaq direct -> Yahoo Finance -> Stooq (etn.us).
- Format: {"symbol":"ETN","price":..,"netChange":..,"pctChange":..,"prevClose":..,
  "quoteTime":"YYYY-MM-DD HH:MM","status":"intraday|postmarket|close","source":"Nasdaq"}.
- The workflow uses `zoneinfo.ZoneInfo("America/New_York")` for the ET wall
  clock (correct across EDT/EST transitions). Cron 13-21 UTC covers
  09:30-17:00 ET in EDT and 08:00-16:00 ET in EST.

## Icon
- eaton.com official favicon.ico (1,406 bytes, 16x16) embedded as data URI.
- eaton.com apple-touch-icon could not be verified (site unreachable from the
  cloud network); use a larger official icon only after verifying its bytes.

## Data baseline
- Price/financials/short/analyst snapshot: 2026-10-01 close ($437.28, +1.76%).
- Q2 2026 (2026-07-31): revenue $8.53B (+21% YoY, +14% organic), adj. EPS $3.15,
  GAAP EPS $2.11; Electrical Americas $4.0B, Electrical Global $2.5B,
  Aerospace $1.2B; electrical backlog +43% YoY, total backlog ~$24.1B;
  FY2026 guidance raised (organic +11-13%, adj. EPS $13.40-13.60);
  Reverse Morris Trust spin-off of Mobility announced (close by 2027Q1).
- Short interest (FINRA 2026-09-15): 7,755,755 shares, 2.00% of float,
  3.9 days to cover (up from 7,208,626 at 8/31).
- Analyst consensus (S&P Global, 28 firms): avg $481.55 / median $488.50;
  11-firm ladder on page (Bernstein $534 top, Barclays $392 Hold at bottom).
- Options (2026-10-01, OptiView only; FlashAlpha had no ETN values):
  dealer GEX positive (+$710.45M), call wall $450, put wall $420,
  max pain $420, P/C OI 1.27, 30d ATM IV 36.9% (rank 43/100).
- Q3 2026 earnings date unconfirmed: MarketBeat/Zacks estimate 2026-11-03
  premarket; OptiView says 11/1 (a Sunday). Marked as pending confirmation.
