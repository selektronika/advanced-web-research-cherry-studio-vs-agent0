---
name: advanced-web-research
description: 'Unified, all-in-one hard-epistemic web research skill for Cherry Studio with Obsidian export. Single skill (no sibling handoffs): run rigorous investigations with labeled confidence, independent cross-checking, adversarial passes, and a method note. Uses Cherry Studio NATIVE tools first — built-in brave-search MCP (brave_web_search / brave_local_search, needs BRAVE_API_KEY in Settings → MCP), mcp__cherry_tools__web_search / web_fetch — plus the currently active research MCP gateway (Exa, Tavily, DuckDuckGo, Wikipedia, time tools) and DaedalMap geography MCP (resolve_point / resolve_bbox / resolve_deep_*), all matched by tool-name suffix, plus Obsidian MCP (vault_write) to export the final report as Obsidian Flavored Markdown to Research/<YYYY-MM-DD>-<task-slug>.md (ledger and sources stay in the conversation workspace). Use whenever the user asks a research question, wants sources or verification, needs current/contested/technical/legal/financial/scientific facts grounded in underlying documents rather than snippets, requests due diligence, market/entity analysis, literature review, or says "latest", "verify this", "what does the evidence say". Do not use for tasks answerable from the user''s own files (use knowledge-base tools) or one-shot lookups a single search settles.'
version: 4.0.0
---

# Advanced Web Research (Unified, with Obsidian Export)

One self-contained skill for every investigation that depends on external evidence. This
file is the orchestrator; the specialized instructions and references live inside this
skill folder — read the relevant one(s) when the task needs them:

```
advanced-web-research/
├── SKILL.md                        # this file — operating loop + routing summary
├── instructions/
│   ├── epistemic-rules.md          # non-negotiable rules, D0–D3 tiers, claim labels, confidence language
│   ├── verification.md             # 4-axis claim classification, independence & counterevidence, ledger
│   ├── reporting.md                # output structure, sources section, self-audit pointers
│   ├── obsidian-export.md          # Obsidian MCP export: report-only, name YYYY-MM-DD-<slug>.md, OFM, procedure
│   └── domain-playbooks.md         # summaries of the 7 domain playbooks (+ pointers to full detail)
└── references/
    ├── tool-routing.md             # verified live tool surface: native Cherry, research gateway, DaedalMap, Obsidian MCP
    ├── evidence-ledger.md          # full ledger schema (claims table, searched-not-found, disconfirming log)
    ├── claim-taxonomy.md           # 4-axis classification, status ladder, standard-per-claim-type hierarchy
    ├── independence-tests.md       # 3 elimination checks, red flags, positive independence indicators
    ├── output-templates.md         # copyable answer templates A/B/C + good/bad lines
    ├── self-audit.md               # mandatory pre-delivery audit checklist
    └── domain/                     # full working detail per domain playbook
        ├── capacity-audit.md       # entity research: unit taxonomy, ownership/control, spec matching
        ├── filing-map.md           # SEC/EU filing navigation, definitions to capture
        ├── stock-flow-workloads.md # market sizing: patterns A–D, traps, script discipline
        ├── rate-verification.md    # rate provenance tests, reconciliation, downtime factors
        ├── registry-sources.md     # candidate authoritative registers by asset family
        └── standards-map.md        # instruments by parameter family, retrieval by jurisdiction
```

Your final response goes directly to the user; no downstream agent corrects your errors.
You own accuracy, source evaluation, uncertainty calibration, disclosed limitations, and a
short method note. Reply in the user's language.

## Operating loop

1. **Frame** — fix the exact question, entities, timeframe, jurisdiction, population,
   definitions, evidence standard. Set the depth tier (D0–D3, see
   `instructions/epistemic-rules.md`). Check durable memory first. Ask at most one
   clarifying question before searching, only if a single ambiguity would materially
   change the conclusion; otherwise assume and disclose material assumptions.
2. **Decompose** — core answer, sub-questions, material claims to verify, likely
   counterarguments, computations. Run sub-questions yourself, batched.
3. **Discover** — batched, varied-wording searches across Brave (native) + Cherry built-in
   + active gateway engines (Exa/Tavily/DDG) + Wikipedia for orientation. Stop on
   saturation. Full tool map: `references/tool-routing.md`.
4. **Retrieve and read** — metadata screen first, then open the underlying page for every
   material claim. Escalate the fetch chain only on failure; disclose escalations.
5. **Evaluate and cross-check** — `instructions/verification.md` + `references/claim-taxonomy.md`
   + `references/independence-tests.md`.
6. **Compute** — nontrivial math via session shell / codemode / python tool, never in your
   head.
7. **Geospatial (if coordinates/places are involved)** — resolve via DaedalMap MCP
   (`resolve_point` → `resolve_deep_point`; `get_catalog` to discover families). See
   `references/tool-routing.md` §C and `instructions/domain-playbooks.md`.
8. **Record** — append verified-claim rows to the ledger per the full schema in
   `references/evidence-ledger.md`. The ledger and source extracts live **only in the
   conversation workspace** (`research-ledger/YYYY-MM-DD-<slug>-ledger.md`,
   `research-sources/YYYY-MM-DD-<slug>/`); only the final report goes to Obsidian.
9. **Calibrate and audit** — labels + confidence per `instructions/epistemic-rules.md`;
   pre-delivery self-audit per `references/self-audit.md`.
10. **Report and export** — structure from `instructions/reporting.md` using the copyable
    shapes in `references/output-templates.md`; export ONLY the final report to Obsidian
    via Obsidian MCP as OFM to `Research/YYYY-MM-DD-<task-slug>.md` (naming convention in
    `instructions/obsidian-export.md`); declare the vault report plus the workspace
    ledger/sources with `report_artifacts`.

## Tool routing in one paragraph

Native Cherry first: `brave_web_search` / `brave_local_search` (built-in brave-search MCP,
needs `BRAVE_API_KEY`), fallback `mcp__cherry_tools__web_search` + `web_fetch`. Then the
active research gateway by suffix: `web_search_exa` / `web_fetch_exa`, `tavily_search` /
`tavily_extract` / `tavily_research` (leads only) / `tavily_map` / `tavily_crawl`,
DuckDuckGo `search`, generic `fetch_content` / `fetch_markdown` / `fetch_json`, Wikipedia
family, `get_current_time` / `convert_time`. DaedalMap by suffix: `get_catalog`,
`get_geography`, `resolve_point`, `resolve_bbox`, `resolve_deep_point`,
`resolve_deep_bbox`. Obsidian MCP by suffix: `vault_write`, `vault_append`, `vault_read`,
`vault_list`, `vault_patch`, `open_file`. Never hard-code server-id prefixes; if a family
is absent, degrade per the table in `references/tool-routing.md` and disclose it.

## Stopping rule

Stop when: the actual question is answered; material claims are verified or their
verification limits are stated; independent corroboration was sought where feasible;
counterevidence and alternative interpretations were considered; dates, jurisdiction,
definitions, and scope were checked; the Obsidian report is saved and the workspace
ledger/sources are written; and further searching is unlikely to change the conclusion. Not at the first plausible answer, and not
to accumulate redundant citations.
