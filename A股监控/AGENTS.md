---
name: A股利好监控系统
description: A-share stock monitoring with dashboard auto-refresh, sentiment analysis, bullish prediction, Telegram bot alerts, and Feishu webhook push
initial_prompt: 帮我搭建一个A股利好监控系统，从同花顺抓取新闻做情绪分析，生成暗色主题监控面板（Hot7热点股、实时利好精选、板块ETF、新闻流），通过飞书Webhook和Telegram Bot推送利好预警及看涨预测，盘中每15分钟自动推送，面板每3分钟自动刷新
---

## Unique Skills
| Skill Name | Purpose |
|------------|---------|
| a-share-monitor | A-share stock monitoring: news fetch, sentiment analysis, dashboard generation with auto-refresh, Telegram bot alerts, Feishu webhook push, multi-target push, credits display, serve mode, bullish stock prediction |

## Project Context

Python + HTML single-page dashboard for monitoring Chinese A-share bullish news. Data from 同花顺 7x24 news API + Tencent quote/K-line APIs. Dark-themed frontend with TailwindCSS + ECharts. Multi-channel push: Telegram Bot (command listener + scheduled) and Feishu Webhook (scheduled cards). Serve mode with built-in HTTP server and auto-refresh.

Stack: Python 3 (requests only), HTML/CSS/JS (single file), TailwindCSS CDN, ECharts CDN, Google Fonts (Noto Sans SC + JetBrains Mono).

## Conventions

- Chinese UI text throughout (Simplified Chinese)
- Red = up/bullish, Green = down/bearish (Chinese market convention)
- Stock codes: 6xx/688xx → sh prefix, 0xx/3xx → sz prefix
- A-share filter: stockMarket in ('22','33','151','17')
- Impact levels: S (>=4), A (>=2.5), B (>=1.5), C (else)
- Telegram messages use HTML parse_mode, auto-chunk at 4000 chars
- Feishu messages use interactive card format (msg_type: interactive)
- Environment variables for config: TG_TOKEN, TG_CHAT_ID, TG_CHANNEL, FEISHU_WEBHOOK, CREDITS_TOTAL, CREDITS_DAILY

## Key Patterns

- THS news API uses tags: '' (all), '-21101' (important), '21109' (opportunity); ctime is Unix timestamp
- Tencent quote API batches up to 30 symbols, pipe-delimited response fields
- Sentiment scoring: BULL_KW/BEAR_KW keyword matching + POLICY_KW/HOT_KW bonus + THS importance field
- Combined sort: `news_impact * recency_factor * (1 + elasticity * 0.1)` where `recency = 1/(1 + age_hours * 0.15)`
- HTML template uses `__PLACEHOLDER__` pattern for data injection (stats, JSON data, credits, run timing, refresh interval)
- Telegram getUpdates long-polling for bot command listening
- `send_telegram()` accepts chat_id as string or list for multi-target push
- Feishu webhook uses `build_feishu_card()` → interactive card with markdown elements + red header
- `build_prediction_section()` scores hot7 + picks candidates: sentiment × position_bonus × streak_bonus × momentum → Top 5 predictions
- Dashboard topbar shows run stats (elapsed time + API call count) and credits remaining
- Auto-refresh: JS timer in template checks market hours client-side, progress bar at bottom

## Workflow

1. Fetch news from 3 THS channels (4 pages each), deduplicate by ID
2. Analyze sentiment, extract stocks/sectors/ETFs, compute Hot7 rankings
3. Fetch Tencent quotes + K-line for related stocks
4. Compute consecutive up streaks, build realtime picks with combined scoring
5. Generate HTML dashboard from template with JSON data injection + run stats
6. Push summary to Telegram targets (Hot7 + Top picks) and/or Feishu webhook
7. Serve mode: HTTP server + periodic refresh (--refresh=N min) + Feishu scheduled push (--feishu-interval=N min)
8. Bot mode: poll getUpdates for "发送" command + 15-min scheduled push during market hours + new bullish news alerts

## Key Decisions

| Decision | Rationale |
|----------|-----------|
| Feishu Webhook over Feishu App Bot | Webhook is simple one-way push; App Bot requires OAuth + event subscription for commands |
| Feishu interactive card format | Rich formatting with markdown, headers, HR dividers; better than plain text |
| --serve mode for dashboard | Combines HTTP server + data refresh in one process; browser auto-reloads |
| 3-min dashboard refresh, 15-min Feishu push | Dashboard needs freshness; Feishu push at lower frequency avoids message fatigue |
| Client-side market hours check | Browser JS checks weekday 9:15-15:00 to pause/resume auto-reload independently |
| Telegram + Feishu simultaneous support | Both configured via env vars; either or both can be active |
| Bot mode (--bot) for Telegram | Combines command listener + scheduled push + alerts in one process |
| Environment variables for credits | User prefers configurable values over hardcoded or API-queried credits |
| Run stats in topbar | Shows API call count and elapsed time for transparency |

## Lessons

- THS API returns non-A-share codes (HK, US); must filter by stockMarket field
- THS ctime is Unix timestamp, not datetime string; use int() conversion
- Telegram sendMessage has 4096 char limit; must auto-chunk long messages at ~4000 chars
- Bot mode must consume existing getUpdates on startup to avoid replaying old commands
- Tencent K-line response key varies between 'qfqday' and 'day'; check both
- `generate_html()` must accept streaks as parameter; relying on global variable fails when called from do_full_summary()
- THS API latency ~1.5s per channel; Tencent quote ~0.2s; K-line ~0.3s; full pipeline ~17-30s
- When editing Python with multiple similar print statements, provide enough surrounding context to uniquely identify the target
- Feishu webhook returns `{"code":0}` or `{"StatusCode":0}` on success; check both fields
- Feishu card markdown supports `**bold**` but not `<b>` HTML tags; use markdown syntax
- Template path in generate_html() uses relative path via `os.path.dirname(__file__)` for portability
- `__REFRESH_INTERVAL__` placeholder set to 0 disables auto-refresh (single-run mode); non-zero enables JS timer
- HTTPServer in serve mode needs `allow_reuse_address = True` (subclass) to avoid `Address already in use` on restart
- Background serve process may appear alive (PID exists) but stop refreshing; monitor dashboard file mtime to detect stale state
- Use `python3 -u` (unbuffered) + `setsid` + redirect to log file for reliable background serve; `nohup` alone may lose output
- Port 8080 cleanup: use `ss -tlnp | grep 8080` to find PID, then `kill -9` before restart
- `is_market_hours()` must use Beijing time (UTC+8) explicitly via `timezone(timedelta(hours=8))`; system timezone may be UTC, causing market hours check to fail silently