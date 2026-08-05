---
name: Read and stream Mudrex market data
description: Pull historical price and mark-price klines over REST and subscribe to live kline, mark-kline and ticker streams over WebSocket — all without authentication.
api: https://trade.mudrex.com/fapi/v1/price
docs: https://docs.trade.mudrex.com/docs/market-data
operations:
  - GET /price/kline
  - GET /price/mark-kline
  - WS /price/ws/linear
generated: '2026-08-04'
method: generated
source: https://docs.trade.mudrex.com/docs/websocket-streams
---

# Read and stream Mudrex market data

This surface is **public and read-only** — no API key, no KYC, no account. It is the
safe place to start with Mudrex, and the only part of the platform you can exercise
without touching live funds.

## Historical klines (REST)

- `GET https://trade.mudrex.com/fapi/v1/price/kline` — OHLCV candles. Up to **25 assets**
  per call and **1440 candles per asset**. Each candle is a 6-element array
  `[open_time, open, high, low, close, volume]`. Unknown or empty symbols are omitted
  rather than erroring the whole call.
- `GET https://trade.mudrex.com/fapi/v1/price/mark-kline` — mark-price candles, same
  shape but **OHLC only** (5-element arrays, no volume).
- Symbols on REST use `<base>/<quote>` — `BTC/USDT`.
- Timestamps on this surface are epoch **seconds**, and values are real JSON **numbers**
  (the authenticated trading API uses milliseconds and strings — do not mix the two).

## Live streams (WebSocket)

Connect to `wss://trade.mudrex.com/fapi/v1/price/ws/linear`.

Every client message uses one envelope:

```json
{ "id": 1, "method": "SUBSCRIBE", "params": ["kline@1m@btcusdt"], "assets": ["btcusdt"] }
```

- `method` is `SUBSCRIBE`, `UNSUBSCRIBE` or `LIST_SUBSCRIPTIONS`.
- `params` carries stream names; `assets` applies **only** to ticker streams.
- Symbols here are **lowercase with no slash** — `btcusdt`. Third symbol format on the
  platform; getting it wrong returns `invalid stream name`.

Available streams: `kline@1s@<symbol>`, `kline@1m@<symbol>`, `markKline@1s@<symbol>`,
`markKline@1m@<symbol>`, `ticker@1s`, `ticker@5s`.

## Rules that will bite you

- **All-or-nothing:** one invalid stream in `params` rejects the entire request and
  changes no subscription state.
- **Keepalive:** the server closes after **40 seconds** of inactivity. PING every ~20s.
  Subscriptions are per-connection and are not persisted — re-subscribe after a reconnect.
- **Limits:** 15 active subscriptions per connection (a ticker stream counts as 1 no
  matter how many assets it tracks), 10 new connections per minute per IP, and 300 REST
  requests per minute per IP. Breaches return `429`.
- The `id` you send is echoed back — it is the only correlation mechanism Mudrex offers
  on either surface.

## Note for tooling

Mudrex publishes no AsyncAPI document for these channels; the catalog captured from the
docs is in `asyncapi/mudrex-market-data-streams.yml`, and the MCP server exposes no
market-data streaming tool.
