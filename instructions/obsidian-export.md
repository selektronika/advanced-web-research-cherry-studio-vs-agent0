# Obsidian Export (via Obsidian MCP)

When a research task produces a final deliverable, export **only the final report** to the
Obsidian vault using the **Obsidian MCP server** tools (match by suffix; server prefix is
instance-specific, e.g. `mcp__578f9352_...__vault_write`):

| Capability | Tool suffix |
| --- | --- |
| Write/create note | `vault_write` — creates missing parent dirs automatically |
| Read note | `vault_read` |
| List folder | `vault_list` |
| Open in UI | `open_file` (optional, to show the user) |
| Structured edit | `vault_patch` |

(`vault_append` exists but is not needed under the current convention.)

## Naming convention

**File name format: `YYYY-MM-DD-<task-slug>.md`** (e.g. `2026-11-13-krakow-terror-attack.md`).

- Date = the day the research is framed/run (`YYYY-MM-DD`, use `get_current_time`).
- Slug = lowercase ASCII, words joined by hyphens, no spaces/underscores
  (e.g. `krakow-terror-attack`, `subsea7-backlog-q3-2026`).

## What goes where

| Artifact | Destination |
| --- | --- |
| **Final report** (OFM) | Obsidian vault: `Research/YYYY-MM-DD-<task-slug>.md` |
| **Evidence ledger** | Workspace only: `research-ledger/YYYY-MM-DD-<task-slug>-ledger.md` |
| **Source extracts** | Workspace only: `research-sources/YYYY-MM-DD-<task-slug>/<source-slug>.md` |

Vault root: `P:\OBSIDIAN` (session workspace path `/mnt/p/OBSIDIAN`).

```text
Obsidian vault:                     Conversation workspace:
Research/                           research-ledger/
└── 2026-11-13-krakow-terror-attack.md   └── 2026-11-13-krakow-terror-attack-ledger.md
                                    research-sources/
                                        └── 2026-11-13-krakow-terror-attack/
                                            └── <source-slug>.md
```

The vault holds only the polished final report. Working material (ledger, source
extracts) stays in the conversation workspace so the vault is not cluttered; declare all
three via `mcp__cherry_tools__report_artifacts` at the end.

## Report format — Obsidian Flavored Markdown

Every report note begins with YAML frontmatter:

```yaml
---
title: "Topic Title"
date: YYYY-MM-DD
created: YYYY-MM-DD HH:mm:ss
tags:
  - research
  - epistemic/D3
  - topic/<domain>
  - status/completed
tier: D3
confidence: high            # high | moderate | limited | low
sources_count: 8
cutoff_date: YYYY-MM-DD
summary: "One-sentence executive resolution."
aliases:
  - "Alt Title"
---
```

Use Obsidian callouts to map research sections:

| Section | Callout |
| --- | --- |
| Executive answer | `> [!summary] Executive Answer` |
| Method & confidence note | `> [!abstract] Method & Calibration Note` |
| Established evidence | `> [!info] Established Evidence` |
| Contradictions / disputed | `> [!warning] Contradictions & Disputed Findings` |
| Red-team counterevidence | `> [!danger] Disconfirming Evidence (Red-Team Pass)` |
| Computations | `> [!example] Computational Validation` |
| Primary source extracts | `> [!quote] Primary Source Extracts` |
| Unresolved / gaps | `> [!question] Unresolved Questions & Missing Data` |

Use wikilinks for entities/concepts (`[[Subsea7]]`, `[[DNV-ST-N001]]`). The companion
ledger is **not** in the vault under this convention — reference it by its workspace path in
the method note (e.g. `workspace: research-ledger/2026-11-13-krakow-terror-attack-ledger.md`).

## Export procedure

1. Compose the full OFM note (frontmatter + callouts + labeled findings + sources).
2. Compute the file name: `YYYY-MM-DD-<task-slug>.md` (today's date + slug).
3. `vault_write` the report to `Research/<YYYY-MM-DD>-<task-slug>.md` (vault-relative).
4. Write the ledger to the workspace at `research-ledger/<YYYY-MM-DD>-<task-slug>-ledger.md`
   and any source extracts under `research-sources/<YYYY-MM-DD>-<task-slug>/` using the
   session file tools (see schema in `references/evidence-ledger.md`).
5. Optionally `open_file` the report so it appears in the Obsidian UI.
6. Declare the report AND the workspace ledger/sources via
   `mcp__cherry_tools__report_artifacts`.
7. Tell the user the vault-relative report path and the workspace paths of ledger/sources.

## Fallback when Obsidian MCP is unavailable

If no `vault_*`/`open_file` tools are exposed this session: write the report with
workspace file tools to `/mnt/p/OBSIDIAN/Research/<YYYY-MM-DD>-<task-slug>.md` (the
mounted vault path), and disclose in the method note that the write went through the
filesystem mount, not the Obsidian MCP. Never claim an MCP export that did not happen.
Ledger and sources still go only to the workspace.
