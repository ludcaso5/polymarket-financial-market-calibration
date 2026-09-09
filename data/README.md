# Data

`05_snapshot_table.csv` is the analysis dataset used in this repository. The filename is preserved from the original data-generation pipeline.

The table was generated from public Polymarket Gamma and CLOB endpoints. It contains binary financial-market outcomes and pre-resolution token-price snapshots at several horizons: 15 minutes, 1 hour, 4 hours, 1 day, 3 days, 7 days, and 14 days.

The main notebook uses only the **1-day (1,440-minute)** snapshots and keeps one observation per market: the lower-priced outcome at that horizon.

## Main fields used

- `market_id` — unique market identifier
- `question` — market question
- `underlying` — inferred financial underlying
- `market_family` — inferred market type
- `resolution_iso` — market resolution timestamp
- `snapshot_horizon_min` — minutes before resolution
- `snapshot_staleness_min` — age of the nearest available price observation
- `price` — implied probability from the token price
- `realized` — resolved binary outcome (0 or 1)
- `calibration_error` — `realized - price`
- `brier` — squared probability error

The original collection pipeline filters resolved binary markets, rejects stale snapshots, and checks that the two outcome prices are approximately complementary before retaining observations.
