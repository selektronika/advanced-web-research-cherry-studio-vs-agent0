# Source Verification & Cross-Checking

Full method references (read when the claim is contested or consequential):
`references/claim-taxonomy.md` (four-axis classification, status ladder, matching standard
to claim type) and `references/independence-tests.md` (the three elimination checks —
shared wire / source of origin / shared dataset — red flags, positive independence indicators).

## Classify every material claim on four axes

1. **Claim type** — factual, causal, statistical, legal, historical, scientific/technical,
   predictive, interpretive, experiential, sentiment, symbolic/traditional, metaphysical.
2. **Evidence type** — official record; primary document; dataset; original research;
   systematic review; technical standard; expert analysis; reputable reporting; testimony;
   community report; social signal; unsupported assertion.
3. **Source relationship** — independent; derivative; same wire/press release; interested
   party; promotional; anonymous; adversarial; methodologically weak.
4. **Epistemic status** — established/documented; strongly supported; moderately supported;
   plausible but limited; disputed; unresolved; unsupported; not meaningfully testable.

## Cross-check procedure

- Seek **two genuinely independent origins** per material claim when feasible — different
  evidence methods and institutional relationships, not just different outlets. Apply the
  three elimination checks from `references/independence-tests.md`; syndication counts as
  one origin.
- Trace repeated reporting to its earliest dated instance.
- Seek counterevidence deliberately with falsification-shaped queries, e.g.
  `"<entity>" AND ("failure" OR "lawsuit" OR "criticism" OR "investigation" OR "retraction")`;
  also seek methodological criticism, corrections, retractions, failed replications.
  Record counterevidence in the ledger even when it doesn't change the conclusion.
- Source hierarchy per claim type (from `claim-taxonomy.md`): a dataset with a published
  method beats an article; an audited filing beats a company summary; a registry beats a
  news estimate; a judgment beats commentary on it. Never accept testimony, prevalence
  language, or marketing for factual, statistical, causal, legal, or financial claims.
- If only one credible origin exists, state that explicitly. If independent verification is
  impossible, lower confidence — never fill the gap with inference.

## Source-quality tests that change weighting

- **Interested party** — a claim about itself is evidence of the claim, not the fact.
- **Provenance of a number** — no retrievable methodology → at best "plausible but limited".
- **Vintage** — a figure's date is part of the claim; state whether a newer figure supersedes.
- **Definition match** — different population/scope/definition does not corroborate.
- **Translation** — machine-translated sources are second-hand.
- **Access level** — full text / abstract / metadata / snippet / second-hand. A conclusion
  built on snippets is a snippet-level conclusion.

## Ledger

Append one row per verified material claim to the ledger using the full schema in
`references/evidence-ledger.md` (claim ID, type, status, root origin & method, source,
URL, access level, vintage, independence assessment, counterevidence, plus
"searched, not found" and disconfirming-evidence sections). The ledger lives **only in the
workspace**: `research-ledger/YYYY-MM-DD-<slug>-ledger.md` (see
`instructions/obsidian-export.md`). The ledger survives
context compaction.
