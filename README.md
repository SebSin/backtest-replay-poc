# Backtest Replay POC

Standalone OHLC bar replay page with tick-by-tick formation, trade markers, and equity curve.

## Usage

Open `static_replay.html` in a browser. No server required — the data file is loaded via `fetch`.

- **Play** — starts streaming bars one step at a time (flat → mid → final OHLC)
- **Pause / Resume** — pauses or resumes the stream
- **Reset** — clears the chart and restarts
- **Speed** — controls animation rate (1–100, multiplied by 16x internally)

## Data

- **11,089 bars** (USATECHIDXUSD, 15m, Dec 1 2025 – May 29 2026)
- **293 trades** from 19f meta-labeling tick-replay backtest (out-of-sample window:
  models trained on data before Dec 1 2025)
- **Equity curve**: $10,000 → $12,680 (+26.8%), Sharpe 2.61, WR 54.9%, MDD -12.9%

### Strategy config (validated champion)

- Meta-labeling 2-stage XGBoost (depth=9, lr=0.08), 19 features
- Retrace-ratio 0.65 labels, 3.0/3.0 ATR barriers, 3h timeout
- 4h SMA(100) trend gate, session filter 13-20 UTC
- Hurdle 0.65, partial TP 2.0 ATR / 50%, 1% risk, friction 1.0, 1s delay

## Files

| File | Description |
|------|-------------|
| `static_replay.html` | Replay page (TradingView Lightweight Charts, dark theme) |
| `static_replay_data.json` | OHLC bars, trades, and equity curve |

## Regenerating the data

From the `pure-price-geometry` repo (models trained strictly before the window):

```bash
.venv/bin/python -m tools.export_replay_meta --start 2025-12-01 --end 2026-05-29
cp plots/static_replay_data.json ../backtest-replay-poc/
```

## License

MIT
