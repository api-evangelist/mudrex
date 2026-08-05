---
name: Manage risk on an open Mudrex position
description: Inspect open positions, attach or amend stop-loss and take-profit, add margin, check the liquidation price, and close, partially close or reverse a position.
api: https://trade.mudrex.com/fapi/v1
docs: https://docs.trade.mudrex.com/docs/positions
mcp: https://mudrex.com/mcp
operations:
  - GET /futures/positions
  - GET /futures/positions/{position_id}/liq-price
  - POST /futures/positions/{position_id}/riskorder
  - PATCH /futures/positions/{position_id}/riskorder
  - POST /futures/positions/{position_id}/add-margin
  - POST /futures/positions/{position_id}/close
  - POST /futures/positions/{position_id}/close/partial
  - POST /futures/positions/{position_id}/reverse
  - GET /futures/positions/history
mcp_tools:
  - get_positions
  - get_liquidation_price
  - place_risk_order
  - amend_risk_order
  - add_margin
  - close_position
  - reverse_position
  - get_position_history
generated: '2026-08-04'
method: generated
source: https://docs.trade.mudrex.com/docs/quick-reference
---

# Manage risk on an open Mudrex position

There is no sandbox. Closing, reversing or re-margining a position realises real PnL.
Ask for explicit confirmation before every write — Mudrex's own MCP documentation marks
`close_position`, `reverse_position`, `place_risk_order`, `amend_risk_order` and
`add_margin` as confirmation-required.

## Steps

1. **List positions.** `GET /futures/positions` returns open positions for **one**
   currency per call (`?trade_currency=INR` for INR; USDT by default). Each item is
   tagged with `trade_currency`. Note the `position_id`, and — if risk orders already
   exist — the `stoploss_order_id` and `takeprofit_order_id`.
2. **Understand the downside.** `GET /futures/positions/{position_id}/liq-price` returns
   the estimated liquidation price, and accepts an optional additional-margin adjustment
   so you can test "what if I add margin" before committing.
3. **Attach protection.** `POST /futures/positions/{position_id}/riskorder` sets
   stop-loss and/or take-profit on a position that has none.
4. **Amend protection.** `PATCH /futures/positions/{position_id}/riskorder`. This
   requires the existing `stoploss_order_id` / `takeprofit_order_id` — fetch them from
   step 1 first, or you get `400 risk order id missing`.
5. **Add or reduce margin.** `POST /futures/positions/{position_id}/add-margin`, in the
   position's own currency. This moves the liquidation price without changing size.
6. **Exit.** `POST /futures/positions/{position_id}/close` closes fully;
   `.../close/partial` closes a portion; `.../reverse` flips LONG↔SHORT in one action.
7. **Review.** `GET /futures/positions/history` for closed positions (one currency per call;
   carries `entry_hedge_rate` / `exit_hedge_rate` on INR-margined positions).

## Rules that will bite you

- Acting on a position that is not open returns `400 Position is not in OPEN state`;
  an unknown id returns `404 Position not found`.
- All of these endpoints are in the **core-trading** rate-limit tier: 10/second,
  500/minute, 30,000/hour, 720,000/day per API key.
- `offset` on the history endpoints is an **end-time boundary in epoch milliseconds**,
  not a row offset. Paging backwards means moving `offset` earlier in time.
- Prices are USDT price levels even when the margin currency is INR.
- No idempotency key exists — a retried close or reverse can double-act. Re-read
  `GET /futures/positions` before retrying anything.

## Related

- Conventions: `conventions/mudrex-conventions.yml`
- Errors: `errors/mudrex-error-codes.yml`
- Rate limits: `rate-limits/mudrex-rate-limits.yml`
