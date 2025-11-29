# Architecture

Objective: single source of truth for signals, with clean visuals and reproducible backtests.

## Layers

- L1: Library (compute-only) — `rb-ta/lib/`
  - Pure functions. No `input.*`, `plot*`, or `log.*`.
  - Modules: smHA, Supertrend, Donchian, DI+/−, HTF helpers, Signals.
  - All HTF requests use `request.security(..., lookahead_off)` with optional confirmation flag.

- L2: Feature Indicators — `rb-ta/ind/`
  - Minimal inputs and visuals per feature for debugging (e.g., `sm-ha-base.pine`).

- L3: Signals Composer Indicator — `rb-ta/ind/signals-composer.pine`
  - Calls features from the library, combines via `signals.pine`.
  - Plots minimal markers. Declares `alertcondition(...)`.

- L4: Strategy Backtester — `rb-ta/strat/`
  - Reuses the same signals as the composer.
  - Adds `strategy.entry/exit` and RM for backtesting.

## Source of Truth

- Indicators and strategies import library functions (or a TV-published library).
- Signals computed in library are reused everywhere (alerts/backtests).

## HTF Safety

- Fetch HTF with `lookahead_off`.
- Gate HTF-based signals with `barstate.isconfirmed`.
- For visuals, “jagged” stepping via HTF close-time alignment boolean.

## Versioning

- Git tags (semver) for repo.
- TradingView library versions increment integer suffix (e.g., `/16` → `/17`).
- `docs/PUBLISHING.md` tracks Git tag ↔ TV library version mapping.
