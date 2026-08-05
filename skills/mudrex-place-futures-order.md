---
name: Place a Mudrex futures order
description: Fund the futures wallet, set leverage for a contract, and place a market or limit LONG/SHORT order with optional stop-loss and take-profit on the Mudrex Futures API.
api: https://trade.mudrex.com/fapi/v1
docs: https://docs.trade.mudrex.com/docs/quickstart
mcp: https://mudrex.com/mcp
operations:
  - GET /wallet/funds
  - POST /wallet/futures/transfer
  - GET /futures
  - GET /futures/{asset_id}
  - POST /futures/{asset_id}/leverage
  - POST /futures/{asset_id}/order
  - GET /futures/orders
mcp_tools:
  - list_futures
  - get_future
  - set_leverage
  - place_order
  - get_orders
generated: '2026-08-04'
method: generated
source: https://docs.trade.mudrex.com/docs/quick-reference
---

# Place a Mudrex futures order

Mudrex has **no sandbox** (API Terms §6.3). Every call below moves real funds on a
live leveraged trading account. Confirm intent with the user before any write.

## Before you start

- The account must have completed KYC (PAN & Aadhaar) and enabled TOTP 2FA.
- You need the API **secret**, sent as `X-Authentication` on every request.
- Base URL: `https://trade.mudrex.com/fapi/v1`. Send `Content-Type: application/json`
  on `POST` / `PATCH` / `DELETE`.

## Steps

1. **Check the wallets.** `GET /wallet/funds` for spot (use `?currency=INR` for the
   INR spot wallet — this endpoint uses `currency`, *not* `trade_currency`).
   `GET /futures/funds` for the futures wallet.
2. **Move margin into futures if needed.** `POST /wallet/futures/transfer` for USDT,
   or `POST /futures/transfers/inr` for INR. These are two different endpoints — sending
   INR to the USDT path returns `400 insufficient balance`.
3. **Find the contract.** `GET /futures` lists tradable contracts;
   `GET /futures/{asset_id}` returns the specification you need before ordering:
   permissible leverage range, min/max price, and the quantity step.
4. **Set leverage.** `POST /futures/{asset_id}/leverage` with the leverage and margin
   type. Leverage is stored **per (asset, currency)** — setting it for USDT does not
   set it for INR. Placing an order against a pair that has never had leverage set
   returns `404 leverage not found`.
5. **Place the order.** `POST /futures/{asset_id}/order`. Append `?is_symbol` to use a
   symbol (`BTCUSDT`) instead of the asset UUID in the path.
   Required body: `leverage`, `quantity`, `order_price`, `order_type` (`LONG` | `SHORT`),
   `trigger_type` (`MARKET` | `LIMIT`). Optional: `is_stoploss` / `stoploss_price`,
   `is_takeprofit` / `takeprofit_price`, `reduce_only`, `trade_currency`.
6. **Confirm.** `GET /futures/orders` (open orders) or `GET /futures/orders/{order_id}`.

## Rules that will bite you

- **There is no idempotency key.** A timed-out `POST .../order` is ambiguous. Never
  blind-retry an order — read back `GET /futures/orders` first and only re-send if the
  order is genuinely absent.
- **Send numbers as strings** (`"0.001"`, `"107526"`). The trading API returns numerics
  as strings to preserve precision. (Market-data endpoints are the exception — real JSON numbers.)
- `quantity` must be a multiple of the asset's quantity step, or you get
  `400 quantity not a multiple of the quantity step`.
- `order_price` must sit inside the asset's min/max, or `400 order price out of permissible range`.
- Omit `trade_currency` and you are trading **USDT** by default.
- Rate limits: order placement is in the core-trading tier — 10/second, 500/minute,
  30,000/hour, 720,000/day per API key. `429` on breach, with no `Retry-After` header.

## Errors

Every REST error is `{ "success": false, "errors": [ { "code", "text" } ] }`. Branch on
`text`, not `code` — `code` mirrors the HTTP status. Full catalog:
`errors/mudrex-error-codes.yml`.
