# Signals Reference

Stable names for booleans/series returned by the library and consumed by indicators/strategies.

## Smoothed Heiken Ashi (smHA)

- Bands (chart TF): `b1*` fast, `b2*` slow.
- Bands (HTF): `b3*` fast, `b4*` slow; “jagged” variants stepped at HTF close.
- Trend flags: `b1Up/b1Dn`, `b2Up/b2Dn`, `b3Up/b3Dn`.
- Midpoints: `b1m/b2m/b3m`.
- Composite categories:
  - `threeUp`, `twoUp`, `oneUp`, `oneDown`, `twoDown`, `threeDown`.
- Zones (price midpoint vs band midpoints):
  - `zonePlusThree`, `zonePlusTwo`, `zonePlusOne`,
  - `zoneMinusOne`, `zoneMinusTwo`, `zoneMinusThree`.
- Cross triggers:
  - `closeCrossesAboveFast1`, `closeCrossesAboveFast2`, `closeCrossesAboveSlow1`.

## Supertrend (ST)

- `up`, `dn`, `trend` ∈ {1, -1}.
- Crossover booleans: `closeCrossesAboveDnLine`, `closeCrossesBelowUpLine`.

## Donchian Channels (DC)

- `upper`, `lower`, `dcMidpoint`.
- Long side: `longPullback`, `longPullbackState`, `longBreakout`.
- Short side: `shortPullback`, `shortPullbackState`, `shortBreakout`.

## DI+/−

- `diPlus`, `diMinus`, `dx`, `adx`, `diHist`.
- Cross booleans:
  - `fastCrossesAboveZero`, `fastCrossesAboveUpperThresh`, `fastCrossesAboveLowerThresh`,
  - `fastCrossesBelowZero`, `fastCrossesBelowUpperThresh`, `fastCrossesBelowLowerThresh`.
- Breaks: `upBreak`, `dnBreak`.

## Composed Examples

- `supertrendLongWindowOpen = trend == 1 and htfTrend == 1`.
- `heikenAshiLongWindowOpen = twoDown or oneDown or oneUp or twoUp`.
- `longHeikenAshiEntry = supertrendLongWindowOpen and (heikenAshiLongWindowOpen or heikenAshiLongWindowOpen[1]) and (closeCrossesAboveFast1 or closeCrossesAboveFast2 or closeCrossesAboveSlow1)`.

## Alerts (indicator)

Expose named booleans via `alertcondition(...)`. Keep titles/messages stable.
- Long Window Open
- Long Trigger
- Short Window Open
- Short Trigger
