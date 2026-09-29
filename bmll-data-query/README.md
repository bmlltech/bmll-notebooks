# bmll.data query notebooks (executed)

Notebooks that call `bmll.data.query` directly, saved **with their outputs** (`.ipynb`) and as
standalone HTML. Each one is scoped to a small universe and date range so that every query fits
the service limits (one minute, 5 GB); the scope is stated at the top of each notebook.

| Notebook | Scope | Executed |
|---|---|---|
| Closing_Auction_Imbalance | AZN / XLON, one closing auction | yes |
| Intraday_Profile | AZN / XLON, one session plus history | yes |
| Market_State_Analysis | AZN / XLON, two sessions | yes |
| Market_Impact_Modelling | HSBA / XLON, ten sessions of trades and level-1 quotes | yes |
| Orderbook_Imbalance_Price_Impact | NDAQ / XNAS, one session of L2 | yes |
| TCA_Using_BMLL | AZN / XLON, 30 synthetic executions | yes |
| VPIN_Analysis | NKE / @SIP, ten sessions of trades | yes |

`Options_Snapshots` is not included: its OPRA reference query returned no contracts, so it did not run.

## How these were produced

Compiled from `bmll-crossenv-notebooks` (`notebooks/*.py`, target `bmll-data-quey`) and executed by
`scripts/validate_bmll_query.py` against production data on 2026-09-29. The query arguments in the
notebooks are the snake_case ones of bmll SDK >= 1.24.16 (`start_date`, `end_date`, ...). Production
still served the previous protocol at that date, so the run used SDK 1.24.15 behind a validation-only
shim that renames those arguments one-to-one (`scripts/bmll_query_compat.py`); the notebooks
themselves are unchanged. Re-run without the shim once the matching service release is live.

Results describe the stated scope only; they are not venue-wide or long-history findings.
