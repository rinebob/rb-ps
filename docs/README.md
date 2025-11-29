# rb-ps Pine Scripts

Utilities, indicators, and strategies for TradingView. Goal: clear visuals and reproducible alerts for manual swing trading (external broker), with a matching strategy for historical analysis.

- **Source of truth (SOT):** Indicators under `rb-ta/ind/`, shared compute under `rb-ta/lib/`.
- **Current focus:** Smoothed Heiken Ashi (smHA), Supertrend, Donchian Channels, DI+/−.

## Repo Structure

```
rb-ta/
  ind/                 # Indicators (plots + inputs + alerts)
    sm-ha.pine         # v6, primary smHA indicator (SOT)
    sm-ha-base.pine    # minimal variant for debugging
  strat/               # Strategies (backtests) reusing the same signals
  lib/                 # Compute-only library modules (to publish to TV)
    rb-ta-lib.pine     # current library; to be split/refined
TV-script-copy/
  11-28-25/            # historical snapshots copied from TradingView (legacy)
docs/
  README.md
  ARCHITECTURE.md
  PUBLISHING.md
  SIGNALS.md
  CHANGELOG.md
```

## Quick Start (TradingView)

1. Open an indicator, e.g. `rb-ta/ind/sm-ha.pine` (Pine v6).
2. Paste into Pine Editor → Save → Add to chart.
3. Choose chart timeframe: Daily (1D), 2D, or Weekly (1W).
   - On 1D or 2D, set HTF input to `W`.
   - On 1W, set HTF input to `M` or `2W`.
4. Configure inputs and (optionally) enable alerts from the indicator’s conditions.

## Non‑Repaint Policy (HTF)

- Fetch HTF with `request.security(..., lookahead_off)`.
- Gate HTF-dependent logic with `barstate.isconfirmed`.
- For visuals, step HTF candles only when chart bar aligns with HTF close.
- Pine v6 note: `plotshape(text=...)` must use const strings; gate visibility via boolean conditions.

## Development Loop

- Edit in IDE → paste into TradingView to verify.
- Keep compute in `lib/` (no inputs/plots/logs). Compose visuals/alerts in `ind/`.
- For backtesting, use a strategy in `strat/` that reuses the exact same signals.

## smHA Summary

- Plots chart‑TF smHA candles (fast/slow) and jagged HTF smHA candles.
- Produces band trend flags, zone classification (±1/2/3), and cross triggers used for entries.
- See `docs/SIGNALS.md` for signal names and alert mapping.

## Versioning

- Git tags (semver) in this repo.
- TradingView library versions increment numeric suffix (e.g., `/16` → `/17`).
- See `docs/PUBLISHING.md` for mapping Git tags ↔ TV library versions.
