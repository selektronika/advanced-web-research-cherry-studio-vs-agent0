# Rate Verification Detail

How to test a rate before it enters a budget or a market figure.

## Provenance tests

1. **Is there a transaction behind it?** An awarded contract, a published tender result, or
   a filing disclosure beats a "market says" figure.
2. **Who is the author, and are they interested?** A broker report and a supplier's own
   price list serve different purposes; both can be Tier 1 or Tier 3 depending on what they
   disclose.
3. **What is the vintage and the market phase?** Rates are cyclical. State the base year;
   if the question's period differs, either find a period rate or present the older one as
   historical.
4. **What exactly is priced?** The same nominal unit can be priced on different bases:
   - calendar vs working day; 24h vs shift vs daylight operation
   - mob/demob included, amortized, or extra
   - fuel, power, and consumables included or on the client's account
   - personnel complement and specialist tooling included or extra
   - standby/idle time and weather day rates
   Compare only like with like, and put the composition in the ledger row.
5. **Is the currency and escalation stated?** No silent conversion; record the rate, the
   date, and the source of any conversion.

## Reconciliation

Cross-check every rate against at least one other origin of a different kind:

- rate vs filing disclosure (operator realized revenue ÷ disclosed vessel-days or units)
- rate vs tender result
- rate vs benchmark publication
- rate vs operator statement

If the reconciliation fails by a material margin, report the range and the reason, not the
convenient number. Reconciliation failures are findings.

## Downtime and availability factors

Downtime converts theoretical capacity into deliverable capacity. Treat it as an explicit,
sourced multiplier set, one per regime:

- **Region and season** (weather windows, ice, monsoon, hurricane season, loop currents)
- **Operational** (maintenance cycles, survey and dry-dock periods, idle periods)
- **Permitting and logistics** (consents, transit, port congestion)
- **Human factors** (crew rotation, bag limits, shift patterns)

Each factor gets a source or an `[Inferred]` label. Where the source is thin, present
Low/Base/High. Never bury availability in a single "efficiency" factor.

## Output discipline

Per rate, in the ledger and in the answer: composition, unit, currency, base year, region,
tier, source with access level, and the uncertainty range. In the answer, a rate table beats
a paragraph, and any single figure used in a downstream calculation must be traceable to a
ledger row.
