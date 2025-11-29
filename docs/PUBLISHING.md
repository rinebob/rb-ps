# Publishing to TradingView

## Goal

Publish a single library that exposes the stable API used by indicators/strategies.

## Steps

1. Prepare `rb-ta/lib/export-library.pine`
   - Aggregate public functions from modules (smHA, ST, DC, DI, signals).
   - No plots, inputs, or logs. Compute only.
2. In TradingView:
   - New script (Library) → paste `export-library.pine`.
   - Name e.g., `rb_TA_lib`.
   - Publish (private or public).
   - Increment version integer each publish (e.g., `/16` → `/17`).
3. Consumers:
   - Import a pinned version: `import rinebob/rb_TA_lib/17 as rb`.
4. Git mapping:
   - Tag Git with semver (e.g., `v1.7.0`).
   - Record mapping below.

## Mapping (Git tag ↔ TV Library)

- v1.0.0 → rb_TA_lib/16
- v1.1.0 → rb_TA_lib/17

## Checklist

- `//@version=6`.
- No `lookahead_on`.
- No plotting or inputs.
- Document tuple return orders.
- Backwards-compatible changes → bump MINOR.
- Breaking changes → bump MAJOR and update consumers.
