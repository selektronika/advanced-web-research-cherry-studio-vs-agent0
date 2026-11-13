# Stock / Flow Workload Detail

Companion to `market-sizing`. Worked detail on the arithmetic patterns that recur in
installed-base and workload questions, and the traps in each.

## Pattern A — installed base → recurring workload

```
workload = stock_units × activity_rate
```

- **Rate source hierarchy**: statutory interval (see `standards-compliance-audit`) →
  operator disclosure → industry benchmark → assumption. Label which.
- **Rate period must match the stock vintage.** A 1-per-year interval applied to a
  point-in-time count gives an annual flow only for the period that count represents.
- **Partial-year activity**: if a unit enters or leaves the base mid-period, weight it by
  time in service, not by one.

## Pattern B — capacity → deliverable workload

A fleet or line count is not a throughput. Convert with:

```
deliverable = Σ_units (available_days × daily_productivity × on_task_share)
```

`on_task_share` and `available_days` need sources (maintenance cycles, idle periods,
contract terms). Where unavailable, use Low/Base/High scenarios.

## Pattern C — market value from volume

```
value = Σ_region volume × price × coverage_share
```

- Price comes from `rates-and-cost-economics` — with currency, vintage, and composition.
- `coverage_share` is extrapolation; state its basis or convert to a scenario.
- Sum by region first; aggregate to total last.

## Pattern D — pipeline / campaign work

Pipeline quantities are `FUTURE_SCENARIO` unless contracts are announced with capacity and
dates. Committed capacity (FID, signed EPC, announced order) is reportable as
`OBSERVED`-adjacent but still forward-looking — label it `[Reported]` with the announced
terms, not as existing workload.

## Common traps

| Trap | Why it breaks | Fix |
| --- | --- | --- |
| Stock counted as flow | An installed count is not annual activity | Show both, with the rate between them |
| Regional sample scaled to global | Sample coverage rarely matches population | State the sampling basis or use a scenario |
| Mandatory interval applied as universal practice | Compliance and practice differ | Split mandatory vs discretionary, by jurisdiction |
| Double counting a shared asset | Same unit reported by two parties | Reconcile by identifier before summing |
| Mixing currencies or vintages | Nominal sums across years | Fix a base year and rate, or keep currency-native |
| Availability buried in one factor | No one can challenge it | List factors separately with sources |
| Point estimate from ranges | False precision | Report Low/Base/High with dominant input |
| Effort and cost conflated | Different drivers | Compute effort first, cost second |

## Script discipline

Keep the computation in one committed script per estimate (`market_<slug>.py`) inside the
ledger folder: inputs at the top as literals or a CSV read, formulas in functions, output a
table with labels per row. Re-running it after an input correction must change only that
input — that is what makes the estimate auditable.
