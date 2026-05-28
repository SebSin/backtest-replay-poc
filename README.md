# Backtest Replay POC

Standalone OHLC bar replay page with tick-by-tick formation, trade markers, and equity curve.

## Usage

Open `static_replay.html` in a browser. No server required — the data file is loaded via `fetch`.

- **Play** — starts streaming bars one step at a time (flat → mid → final OHLC)
- **Pause / Resume** — pauses or resumes the stream
- **Reset** — clears the chart and restarts
- **Speed** — controls animation rate (1–100, multiplied by 16x internally)

## Data

- **8,704 bars** (USATECHIDXUSD, 15m, Dec 25 2025 – May 18 2026)
- **169 trades** from live tick-replay backtest (XGBoost, 3.0 ATR, 0.45 hurdle, max_overlap=1)
- **Equity curve**: $10,000 → $20,687 (+107%), Sharpe 9.58

## Files

| File | Description |
|------|-------------|
| `static_replay.html` | Replay page (TradingView Lightweight Charts, dark theme) |
| `static_replay_data.json` | OHLC bars, trades, and equity curve |

## License

MIT
