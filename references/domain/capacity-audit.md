# Capacity Audit

How to turn "the company has 12 vessels / 3 plants / 500 engineers" into a defensible
capacity statement. Domain-neutral: substitute the unit (vessel, plant, line, vehicle, site,
license) — the structure is the same.

## Unit taxonomy rules

- **One unit = one row.** A unit is counted once, by its canonical identifier (IMO, hull
  number, registration, asset tag). Never count a group photo as a fleet list.
- **Unit class matters.** A unit of class A and a unit of class B are not interchangeable:
  record the specification that determines what the unit can do (tonnage, depth rating,
  deck area, crane capacity, slots, throughput, class, jurisdiction).
- **Status is part of the record.** `OPERATIONAL`, `UNDER_CONSTRUCTION`, `APPROVED / FID`,
  `ON_HIRE`, `IDLE`, `DECOMMISSIONED`. A count that ignores status is not a capacity count.
- **Vintage year is part of the record.** Fleet counts from a marketing page decay; prefer
  the vintage that matches the question's period.

## Ownership / control reconciliation

For each unit, record the control basis and its source:

| Basis | What it supports | What it does not support |
| --- | --- | --- |
| Owned | Long-term capability | Nothing further |
| Long-term charter (multi-year) | Capability, with term dates | Assumed continuation past term |
| Short-term / spot charter | Opportunistic capability | Planned workload |
| Managed / operated for others | Capability **with** the asset | Counting it twice in the same market |
| Agency / distributor / partner | Access, not capacity | Capability claims |

Double counting is the most common error: a unit operated for a partner and reported by both
partners is one unit. Where a status is ambiguous, mark it ambiguous rather than choosing.

## Specification-to-demand matching

Capability is a match, not a number. Before using a count in any workload or market figure,
check:

1. Class / rating requirement of the task (e.g. a depth rating, a class certificate, a
   pressure rating, a certification).
2. Geographic access (theater, distance to base, port, ice, permit).
3. Availability (maintenance periods, survey cycles, idle-iron periods).
4. Tooling and personnel complements that travel with the unit.
5. Contract state (committed vs open).

State which of these were verified and which were assumed. Unverified availability is an
assumption, and assumptions go in the answer.

## Utilization and coverage

- Utilization is fleet-state-dependent: published utilization for one operator is not a
  market average, and "on hire" is not "utilized at full rate".
- Coverage percentages need a denominator and a period ("share of X in year Y, measured by
  Z"), plus a source. Without all three, label `[Reported]`.
- Any conversion (vessel-days to work units, shifts to units) is a computation: run it with a
  script and record the formula and assumptions.

## Handoff

Reconciled unit tables feed `market-sizing` (as the asset base input) and
`rates-and-cost-economics` (as spread composition), and every row lands in the evidence
ledger with its source and access level.
