# Domain Playbooks (apply when the question touches these)

Each playbook below is a summary; the full working detail lives in `references/domain/` —
read the matching file when the question needs it:

| Domain | Full reference |
| --- | --- |
| Entity / capacity | `references/domain/capacity-audit.md` |
| Financial filings | `references/domain/filing-map.md` |
| Market sizing | `references/domain/stock-flow-workloads.md` |
| Rates & cost | `references/domain/rate-verification.md` |
| Registries & assets | `references/domain/registry-sources.md` |
| Standards & compliance | `references/domain/standards-map.md` |

## Entity research
Separate what the entity IS from what it CLAIMS: legal identity/parent (corporate
register, ticker), operating divisions, contract forms, physical assets and capacity with
identifiers, segment economics tied to the relevant activity, footprint, claims vs
evidence. Never extrapolate group totals to a division; distinguish owned/chartered/managed;
marketing is `[Reported]`; state vintages of headcount/fleet counts.

## Financial filings (detail: `references/domain/filing-map.md` — SEC item map, European reports, definitions to capture, "a press release is not a filing")
Identify the filing (form, filer, period, amended/restated), fetch and archive the
original, navigate by section (Item 1/1A, 7, 8; segment note; IFRS 15 / ASC 606 backlog
note), extract with value + currency + unit + period + basis + audited flag + exact line
item + source locator. Never fill gaps by inference (`<REQUIRED_FROM_SOURCE>`); never mix
bases or currencies silently; guidance is `[Reported]` forecast, not fact.

## Market sizing (detail: `references/domain/stock-flow-workloads.md` — patterns A–D, trap table, script discipline)
No mental math (script it); inputs carry provenance (value + unit + definition + vintage +
source); separate stock vs flow and run-rate vs pipeline; label every quantity `OBSERVED` /
`CALCULATED` / `EXTRAPOLATED` / `FUTURE_SCENARIO`; use Low/Base/High scenarios instead of
single points; state availability/downtime factors with sources; aggregate last.
Core formulas:
```
units_per_period  = stock_units × activity_rate (1/period)
effort_periods    = units_per_period × effort_per_unit
vessel_days       = effort_periods / daily_productivity × (1 + downtime_factor)
cost_period       = vessel_days × spread_day_rate
market_value      = Σ_region cost_period × coverage_share
```

## Rates and cost economics (detail: `references/domain/rate-verification.md` — provenance tests, reconciliation, downtime factors)
Define the unit of cost and calendar basis; decompose the spread (base rate + tooling +
crew + consumables + logistics/mob-demob) — never a naked day rate; record contract
structure and fuel responsibility; verify the asset spec exists; apply region/season
downtime factors with sources; tier every rate (Tier 1 tender/award/audited filings; Tier 2
recognized broker/benchmark bodies; Tier 3 trade press → `[Reported]`); never average
across tiers; state base year and currency.

## Registry asset intel (detail: `references/domain/registry-sources.md` — candidate registers by asset family, register-selection checklist)
Define the asset class and unit of count first; prefer official statutory registers >
classification societies > operator disclosures > industry databases > news; capture the
identifier (IMO/MMSI, license/block ID, coordinates with datum) and status + as-of date
(`OPERATIONAL`, `UNDER_CONSTRUCTION`, `APPROVED/FID`, `IDLE`, `DECOMMISSIONED`); archive
the register page; reconcile across two registers and report both numbers when they
disagree — never average; derived counts are `CALCULATED`.

## Standards and compliance (detail: `references/domain/standards-map.md` — instruments by parameter family, retrieval targets by jurisdiction, citation discipline)
Name the governing instrument per jurisdiction; fetch the instrument itself, never a blog
interpretation; verify edition/revision/status; cite document + edition + clause + table +
page, quoting the operative sentence; classify mandatory vs recommended vs discretionary
(statute > licence condition > class rule > contract > guidance); present cross-jurisdiction
differences side by side; label derived workload `CALCULATED` with the interval as input.

## Geospatial regionalization (DaedalMap MCP)
Resolve coordinates/place names to stable administrative or marine region ids
(loc_id-style keys, EEZ/sea basin) using the DaedalMap geography MCP tools (see
`references/tool-routing.md` → DaedalMap section): `resolve_point` (GLOBAL administrative
→ Admin0; ISO3 scope → shallow country bank; MARINE requires one specific family such as
`exclusive_economic_zone` or `water_body` with `water_kind`), `resolve_bbox`, then
`resolve_deep_point` / `resolve_deep_bbox` with the returned `shallow_loc_id` for Admin
1–6. Discover families via `get_catalog(catalog='geometry')`. Keep offshore points exact
(WGS84 unless stated); never snap to a convenient nearby country. Without the plugins,
disclose that region keys could not be resolved.
