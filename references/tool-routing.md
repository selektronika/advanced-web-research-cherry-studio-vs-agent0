# Tool Routing — Verified Live Tool Surface (2026-11)

Read the live tool schema before the first call in a session; the runtime schema is
authoritative for parameter names. Identify tools by their **name suffix** — server-id
prefixes (e.g. `mcp__578f9352_...__`) are instance-specific and must never be hard-coded.

## A. Cherry Studio native tools (always try first — no Docker gateway needed)

| Capability | Tool suffix | Notes |
| --- | --- | --- |
| Brave web search (built-in `brave-search` MCP) | `brave_web_search` | Requires `BRAVE_API_KEY` in Settings → MCP env. `query`, `count` (1–20), `offset`. |
| Brave local/places | `brave_local_search` | Falls back to web search when no local results. |
| Cherry built-in search | `mcp__cherry_tools__web_search` | Always-on fallback; returns citation ids → `[cite:id]`. |
| Cherry built-in fetch | `mcp__cherry_tools__web_fetch` | Batch up to 20 URLs per call; returns citation ids. |
| Time | `get_current_time`, `convert_time` (suffix match; exposed via gateway) | Compute exact date ranges before time-relative searches. |
| Computation | session shell (`uv run python`, `bun`), `codemode`, `python_execute` | All nontrivial math by script, never in your head. |
| Durable memory | `mcp__agent_memory__memory` | `search` before re-asking; `update` for durable lessons only. |
| User's own documents | knowledge-base tools (`kb_list`/`kb_search`/`kb_read`) when exposed | Check BEFORE the web when the answer should come from the user's files. |
| Local documents | `mcp__cherry_tools__to_markdown` | Convert local PDF/Office; source never modified. |
| Deliverables | `mcp__cherry_tools__report_artifacts` | Declare final saved files at the end. |

## B. Research MCP gateway (currently active in this session — suffix match)

| Capability | Tool suffix | Notes |
| --- | --- | --- |
| Semantic search | `web_search_exa` | Describe the ideal page; `category:company`/`category:people` for entities. |
| Full-page fetch | `web_fetch_exa` | Raise `maxCharacters` when truncated. |
| Scoped/deep search | `tavily_search` | `include_domains`, `start_date`/`end_date`, `time_range`, `country`. |
| URL extraction | `tavily_extract` | `extract_depth: advanced` for tables/protected pages. |
| Multi-source synthesis | `tavily_research` | Rate-limited; output is a **lead set, never evidence**. |
| Site structure | `tavily_map`, `tavily_crawl` | Only for bounded site-structure questions. |
| DuckDuckGo search | `search` (DDG server) | Independent engine for batch diversity. |
| Generic fetch | `fetch_content`, `fetch_markdown`/`fetch_html`/`fetch_json`/`fetch_txt` | Paginate with `start_index`/`max_length`; `backend: curl` bypasses some bot filters. |
| Wikipedia | `search_wikipedia`, `get_summary`, `get_sections`, `get_article`, `get_links`, `get_related_topics`, `extract_key_facts`, `get_coordinates` | Orientation only — never final evidence for contested claims. (Some builds expose a duplicate mangled-suffix copy, e.g. `wikipedia_ex_*` — same tools, don't double-count.) |
| Time | `get_current_time`, `convert_time` | |
| Sequential thinking | `sequentialthinking` | Private scratch only; never evidence, never narrated. |

## C. DaedalMap geography MCP (2 instances active — suffix match, use either)

| Capability | Tool suffix | Contract highlights |
| --- | --- | --- |
| Catalog | `get_catalog(catalog='geometry' \| 'data')` | Lists families/scopes/packs; baseline 252 entities to Admin 2; deeper tiers for AU, BR, CA, FR, DE, MX, UK, US. |
| Geography metadata | `get_geography` | Coverage/editions for one family or scope. |
| Point resolve (shallow) | `resolve_point` | `scope_id`: `GLOBAL` (Admin0) or ISO3 country, or `MARINE` with one family (`exclusive_economic_zone`, `territorial_seas`, `high_seas`, `water_body` + `water_kind=named\|zone`). Supports point arrays with `id`/`row_index`. |
| BBox resolve (shallow) | `resolve_bbox` | 4 WGS84 corners, no antimeridian crossing; best equal-area overlap per level + loc_id. |
| Deep point | `resolve_deep_point` | After `resolve_point`: pass original coords + `shallow_loc_id` + optional `family` (default `administrative`) → Admin 1–6. |
| Deep bbox | `resolve_deep_bbox` | Same pattern for rectangles. |

Rules: no call crosses scopes or opens another family's bank; keep coordinates exact
(WGS84); a point is not an extent; offshore points resolve to EEZ/marine families, never
snapped to a nearby country.

## D. Obsidian MCP (active in this session — suffix match)

| Capability | Tool suffix | Notes |
| --- | --- | --- |
| Write/create note | `vault_write` | Creates parent dirs; text only; `ifNoneMatch: '*'` = create-only. |
| Append | `vault_append` | Creates file if missing. |
| Read / list / map | `vault_read`, `vault_list`, `vault_get_do_*` | `vault_read` returns content + frontmatter + links + `version` token. |
| Structured edit | `vault_patch` | heading/block/frontmatter targets; use `ifMatch` with the version token. |
| Open in UI | `open_file` | Opens (or creates) the note in Obsidian. |
| Search | `search_simple`, `search_query` (JsonLogic over note metadata) | |
| Events (SSE) | `events_get_l_*` | Only when live event streaming is needed. |

Export targets: see `instructions/obsidian-export.md` — final report ONLY to the vault at
`Research/<YYYY-MM-DD>-<task-slug>.md` (vault-relative; vault root `P:\OBSIDIAN`); ledger
and source extracts stay in the workspace (`research-ledger/`, `research-sources/`).

## Batching & saturation

- No `parallel` tool: **emit several independent research calls in one assistant
  message**. Split fan-outs over ~8 calls into successive batches.
- Vary wording AND engine per batch (Brave exact terms, Exa semantic, Tavily domain-scoped,
  DDG/Cherry fallback, Wikipedia for orientation).
- Stop on saturation: two consecutive searches with no new distinct origin. Deduplicate by
  URL **and** underlying origin (wire copy, press release, shared dataset).
- Query language: English default; jurisdiction's language when local law/business dominates;
  native + English pair for contested claims at D2+.

## Fetch chain (escalate only on failure/thin content; disclose escalations)

1. Metadata screen of candidates.
2. `mcp__cherry_tools__web_fetch` / `web_fetch_exa` / `tavily_extract` (basic) / `fetch_content`.
3. Re-fetch with higher `maxCharacters`, `extract_depth: advanced`, or `backend: curl`.
4. Interactive browser (cherry-browser) only if exposed AND the page needs JS/auth.

## Degradation table

| Missing | Do instead | Disclose |
| --- | --- | --- |
| Brave built-in (no BRAVE_API_KEY) | Cherry `web_search` + Exa/Tavily/DDG | engines actually used |
| Whole research gateway | Cherry `web_search` + `web_fetch` | engine list in method note |
| DaedalMap | Plain-HTTPS geography fallback or skip | region keys unresolved |
| Obsidian MCP | Filesystem write to `/mnt/p/OBSIDIAN/Research/...` | export via mount, not MCP |
| No fetch tools | Snippet-level work | conclusions are snippet-level |
| No session shell | Formula + inputs shown | computations not machine-verified |
| No delegation tools | Self-run sub-questions and D3 pass | independence self-checked |
