# Evidence Ledger — Schema and Rules

The evidence ledger is a durable markdown file maintained during an investigation. It records
every material claim with its epistemic status, root origin, and counterevidence. It survives
context compaction and lets anyone audit the final report claim by claim.

## Location and naming

- **The ledger lives ONLY in the conversation workspace** (never in the Obsidian vault):
  `research-ledger/YYYY-MM-DD-<task-slug>-ledger.md` under the current workspace, using the
  same `YYYY-MM-DD-<task-slug>` name as the final report.
- Only the final report is exported to Obsidian (see `instructions/obsidian-export.md`);
  the report's method note references the ledger by its workspace path.
- Initialize the ledger as soon as primary retrieval begins; append rows as claims are verified or contested.

## Ledger structure

```markdown
# Evidence Ledger: <Topic Name>

- **Inquiry:** <exact question as framed>
- **Depth Tier:** D0 | D1 | D2 | D3
- **Framed Date:** YYYY-MM-DD
- **Effective Research Cutoff:** YYYY-MM-DD
- **Definitions Fixed:** <term = definition>
- **Associated Report:** `Research/YYYY-MM-DD-<task-slug>.md` in the Obsidian vault (workspace path of this ledger: `research-ledger/YYYY-MM-DD-<task-slug>-ledger.md`)

## Material Claims Ledger

| Claim ID | Claim Summary | Claim Type | Epistemic Status | Root Origin & Method | Source & Citation | URL / Accession | Access Level | Vintage | Independence Assessment | Counterevidence Found |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| C-01 | <claim> | Factual / Statistical / Legal / ... | [Documented] | <e.g. class society register record> | [S1] <source> | <url> | Full text | YYYY-MM | <independent authoritative register> | <none found / what was found> |

## Searched, Not Found
- Expected records/licenses/datasets systematically searched for but not surfaced, e.g.
  "state registry query for active operating permit — no active permit found."

## Disconfirming Evidence Log
- Counterevidence found by the adversarial pass (delegated or self-run), with vectors used,
  e.g. "litigation vector: pending suit filed YYYY-MM".

## Open Ambiguities & Limitations
- Unresolved questions, proprietary boundaries, and assumptions that could alter conclusions.
```

## Rules

- One row per **material** claim; surface in the ledger only what changes the answer or its label.
- Record how many **genuinely independent origins** support each claim and name the weakest link.
- Two independent origins with a disclosed single-origin caveat beats ten derivative pages.
- Source extracts likewise stay in the workspace: `research-sources/YYYY-MM-DD-<task-slug>/<source-slug>.md`.
- Transfer only **durable lessons** (a registry moved URL, a provider requires specific query
  formatting) to persistent agent memory; never dump ephemeral project claims into it.
