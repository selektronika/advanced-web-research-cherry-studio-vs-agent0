
---
name: a0-mcp-bridge
description: Delegate tasks to Agent Zero via MCP. Activate on A0/agent-zero mentions or when task needs shell, filesystem, browser, code execution, or subordinate agents.
tags: [agent-zero, mcp, delegation]
version: 3.1.0
---

# A0 Bridge

## MCP Tools (from `tools/list` — use discovered prefixed names)

| Tool | Params | Does |
|------|--------|------|
| `send_message` | `message` (str, req) | Send instruction, blocks until A0 responds |
| `finish_chat` | — | Close session. **Always call.** |

## Gate

DELEGATE when: shell · filesystem · browser · code sandbox · A0 sub-agents · multi-step autonomous · parallel research via Swarm.
KEEP LOCAL when: web search + fetch + calc suffices · KB query · single-step · low latency.

## Protocol

**1 · Frame** — First `send_message` is self-contained (A0 has NO Cherry context):


Optional Swarm hint (when task is parallelizable):


**2 · Iterate** — Read response before next send. Max 10 turns.
- Clarification asked → answer specifically
- Partial result → request remainder
- Error → simplify, retry
- Loop → "STOP. Summarize progress. What blocks you?"

**3 · Close** — `finish_chat` after final output or abandonment.

## A0 Internal Capabilities (Cherry does NOT call these directly)

Agent Zero has rich internal tools. Cherry's `send_message` is the **only
interface** — but knowing A0's capabilities shapes better task instructions.

**Swarm (delegate_parallel):**
- Fans out independent sub-tasks to parallel workers
- Params per task: `task` (req), `label`, `profile`, `endpoint`
- Max 16 concurrent workers (default 4)
- 64 KB result cap per worker (configurable to 1024 KB)
- Workers start **fresh** — no parent conversation history
- Nesting blocked — one delegation layer per run
- Workers can message each other via `swarm_message`

**When to instruct A0 to use Swarm:**
- Comparing N alternatives in parallel (frameworks, providers, regions)
- Multi-source research (each worker researches one source)
- Batch file processing (each worker handles a subset)
- Any task decomposable into independent sub-tasks

**Other A0 tools** (available internally):
- `code_execution_tool` — Python/shell in sandboxed Docker
- `call_subordinate` — sequential specialist delegation
- Browser automation, filesystem ops, knowledge base, memory

**Profile system:** A0 supports per-task profile overrides controlling
which tools/MCP servers/skills each worker can use. If you need a
constrained execution, include in your message:


## Validate before presenting to user

Completeness · Coherence · Sources cited · Format matches request.
Fail → correction via `send_message` before closing.

## Errors

| Signal | Action |
|--------|--------|
| Connection refused | A0 down — check container |
| 405 | Switch to `streamableHttp` |
| Timeout | A0 busy — wait, retry once |
| Empty response | Retry once → new session |
| A0 loops | Send STOP redirect |
| Response >64KB truncated | Break task into smaller chunks |
| 3 consecutive failures | Abandon, Cherry-local fallback |

## Rules

- Messages must work WITHOUT Cherry conversation history
- Name everything explicitly — no pronouns, no "the file"
- One deliverable per message preferred
- A0 filesystem ≠ Cherry filesystem (Docker boundary)
- Swarm workers inherit parent profile unless overridden
- Swarm nesting is blocked — don't ask A0 to nest swarms
- Never send conversation dumps as context
- Never skip `finish_chat`

