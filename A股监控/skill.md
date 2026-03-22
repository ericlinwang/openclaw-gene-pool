---
name: a-share-monitor
description: Build and customize A-share (China) stock monitoring systems with news sentiment analysis, realtime quotes, dark-themed dashboard with auto-refresh, and multi-channel push (Telegram Bot + Feishu Webhook). Use when user wants to monitor Chinese A-share stocks, fetch 同花顺 financial news, analyze bullish/bearish sentiment, generate trading dashboards, or set up Telegram/Feishu alerts for stock market events. Triggers on mentions of A股, 同花顺, 利好监控, stock monitoring dashboard, or Chinese stock market tools.
---

# A-Share Monitor

Build A-share stock monitoring tools: news fetching, sentiment analysis, HTML dashboard with auto-refresh, Telegram bot integration, and Feishu webhook push.

## Bundled Assets

- `assets/fetch_stocks.py` — Complete Python backend (news fetch, quote fetch, K-line, sentiment analysis, HTML generation, Telegram push, Feishu webhook push, Bot mode, Serve mode with auto-refresh)
- `assets/template.html` — Dark-themed dashboard template (TailwindCSS + ECharts + Noto Sans SC) with Hot7, realtime picks, sector/ETF panels, night news, full news feed with tabs, auto-refresh progress bar

Copy these to the user's output directory as starting points. Customize as needed.

## Environment Variables

| Variable | Purpose |
|----------|---------|
| `TG_TOKEN` | Telegram Bot token |
| `TG_CHAT_ID` | Private chat ID for push |
| `TG_CHANNEL` | Channel username (e.g., `@channel_name`) for simultaneous push |
| `FEISHU_WEBHOOK` | Feishu bot webhook URL for push |
| `CREDITS_TOTAL` | Total remaining credits (displayed on dashboard) |
| `CREDITS_DAILY` | Estimated daily credit consumption (displayed on dashboard) |

## Key APIs

| API | Endpoint | Notes |
|-----|----------|-------|
| THS News | `https://news.10jqka.com.cn/tapp/news/push/stock/?page_size={n}&track=website&tag={tag}&page={p}` | Tags: `''` (all), `'-21101'` (important), `'21109'` (opportunity) |
| Tencent Quotes | `https://qt.gtimg.cn/q={symbols}` | Pipe-delimited fields, batch up to 30 |
| Tencent K-line | `https://web.ifzq.gtimg.cn/appstock/app/fqkline/get?param={symbol},day,,,{days},qfq` | Forward-adjusted daily K-line |
| Telegram Bot | `https://api.telegram.org/bot{token}/sendMessage` | HTML parse_mode, 4096 char limit |
| Telegram Updates | `https://api.telegram.org/bot{token}/getUpdates` | Long-polling for command listening |
| Feishu Webhook | `https://open.feishu.cn/open-apis/bot/v2/hook/{id}` | Interactive card format, POST JSON |

## Stock Code Mapping

- `6xxxxx` / `688xxx` → `sh{code}` (Shanghai)
- `0xxxxx` / `3xxxxx` → `sz{code}` (Shenzhen)
- Filter A-shares only: `stockMarket in ('22','33','151','17')`

## Chinese Convention

- **Red = up (bullish)**, **Green = down (bearish)** — opposite of Western markets

## Sentiment Analysis

- `BULL_KW` / `BEAR_KW` keyword arrays score each news item
- `POLICY_KW` (政策) and `HOT_KW` (热点) provide bonus scores
- THS `import` field ≥ 3 and `color == '2'` boost bullish weight
- Impact levels: S (≥4), A (≥2.5), B (≥1.5), C (else)
- Combined score: `news_impact × recency_factor × (1 + elasticity×0.1)`

## Run Modes

```bash
# Dashboard only (single run)
python3 monitor.py

# Dashboard + Telegram + Feishu push
TG_TOKEN=xxx TG_CHAT_ID=xxx FEISHU_WEBHOOK=xxx python3 monitor.py

# Serve mode: HTTP server + auto-refresh dashboard + Feishu scheduled push
FEISHU_WEBHOOK=xxx python3 monitor.py --serve --refresh=3 --feishu-interval=15 --port=8080

# Watch mode (new bullish news alerts via Telegram)
TG_TOKEN=xxx TG_CHAT_ID=xxx python3 monitor.py --watch --interval=120

# Bot mode (Telegram: command listener + 15min scheduled push + alerts)
TG_TOKEN=xxx TG_CHAT_ID=xxx python3 monitor.py --bot
```

### Serve Mode Details

- `--serve`: Starts built-in HTTP server + periodic data pipeline refresh
- `--refresh=N`: Dashboard data refresh interval in minutes (default 3)
- `--feishu-interval=N`: Feishu push interval in minutes (default 15)
- `--port=N`: HTTP server port (default 8080)
- Browser auto-refreshes during market hours (9:15-15:00) with progress bar
- Rest hours: browser pauses refresh, shows "休市中" status

### Feishu Push

- Uses interactive card format (`msg_type: interactive`) with red header
- Contains Hot7 + Top 10 realtime picks + Top 5 bullish predictions with prices, change %, streaks
- `build_prediction_section()` computes prediction scores from hot7 + picks data (sentiment × position × streak × momentum)
- `build_feishu_card()` builds the card (now includes prediction section), `send_feishu()` posts to webhook
- `do_feishu_push()` is the high-level wrapper

## Multi-Target Push

- Telegram: `send_telegram()` accepts `chat_id` as string or list
- Feishu: `send_feishu()` posts to single webhook URL
- Both can be active simultaneously via env vars

## Dashboard Run Stats

Topbar displays API call count, elapsed time, and credits via `__PLACEHOLDER__` pattern. Auto-refresh interval injected via `__REFRESH_INTERVAL__`.