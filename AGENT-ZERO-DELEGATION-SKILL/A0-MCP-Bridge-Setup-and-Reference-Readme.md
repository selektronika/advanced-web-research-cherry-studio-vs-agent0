
# A0 MCP Bridge — Setup & Reference

> NOT loaded into prompt. Read once during setup.

---

## Architecture



A0 is natively MCP **client-only** (Issue #359). Your custom MCP server
wrapper bridges the gap by exposing `send_message` + `finish_chat`.
Cherry Studio talks to the wrapper; the wrapper talks to A0's HTTP API.

## Installation



## Cherry Studio MCP Config

Settings → MCP → MCP Servers → JSON Import:

```json
{
  "mcpServers": {
    "agent-zero": {
      "type": "streamableHttp",
      "url": "http://localhost:PORT/mcp"
    }
  }
}

{
  "mcpServers": {
    "agent-zero": {
      "type": "streamableHttp",
      "url": "http://localhost:PORT/mcp",
      "headers": { "Authorization": "Bearer TOKEN" }
    }
  }
}

"type": "sse"
.../mcp/sse
agent-zero.send_message
agent-zero.finish_chat
docker ps
agent-zero
a0-mcp-bridge
http://localhost:PORT/mcp
http://host.docker.internal:PORT/mcp
http://IP:PORT/mcp
https://a0.domain.com/mcp
task
label
profile
endpoint
delegate_parallel
→ send_message("TASK: List Python files importing pandas in /src
DELIVERABLE: JSON array of paths")
← ["/src/etl.py", "/src/analysis.py"]
→ finish_chat

→ send_message("TASK: Compare cloud GPU pricing across 4 providers
CONTEXT: AWS, GCP, Azure, Lambda Labs — A100, H100 — EU region
DELIVERABLE: Markdown table with $/hr and source URLs
EXECUTION: Use delegate_parallel — one worker per provider
RULES: Official pricing pages only, flag stale >30d")
← table (A0 internally fans out 4 workers)
→ finish_chat

→ send_message("TASK: Merge CSVs in /data/input/ on 'id', dedup, export to /data/merged.csv
DELIVERABLE: code + row counts before/after
RULES: pandas, handle encoding errors")
← code + results
→ finish_chat

→ send_message("TASK: Security audit /workspace/myapp
PROFILE: security-auditor
DELIVERABLE: Markdown report with severity table
EXECUTION: Use delegate_parallel:
  - Worker 1: pip-audit dependencies
  - Worker 2: grep hardcoded secrets
  - Worker 3: check file permissions")
← consolidated report
→ finish_chat

→ send_message("TASK: Design a caching strategy for FastAPI + PostgreSQL
CONTEXT: 10k req/min peak, 80% hit same 500 endpoints, data changes every 5-15 min
DELIVERABLE: Architecture overview with layer recommendations")
← architecture proposal
→ send_message("Go deeper on Redis layer: eviction policy + invalidation on DB writes")
← detailed Redis config
→ send_message("Write the FastAPI caching middleware based on our discussion")
← code
→ finish_chat

ECONNREFUSED
docker ps
405
Error? → Retryable? → Wait + retry → Still failing?
  → Reformulate + new session → 3rd failure?
    → Abandon, Cherry-local fallback

/a0/usr/agents/<profile-id>/
agent.yaml                    ← identity config
prompts/                      ← system prompt overrides
plugins/
  _model_config/config.json   ← LLM settings
  _tool_access/config.json    ← tool/MCP policies
  _skills/config.json         ← skill visibility

local:<tool>
plugin:<id>:<tool>
mcp:<server>:<tool>
