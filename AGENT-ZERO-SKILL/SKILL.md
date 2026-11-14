---
name: cherry-studio-bridge
description: 'Cherry Studio MCP Research Bridge for Agent Zero. Activate when Cherry Studio contacts via MCP for research assistance. Detects research queries, routes to advanced-web-research, and optimizes workflow for efficient execution. Handles both direct research requests and Cherry Studio intermediary communication.'
version: 1.0.0
trigger_patterns:
  - cherry studio
  - cherry-studio
  - mcp research
  - research assistance
  - research bridge
  - external research request
  - third party research
tags:
  - cherry-studio
  - mcp
  - research
  - bridge
  - integration
---

# Cherry Studio MCP Research Bridge

This skill activates when Cherry Studio (or any external MCP client) contacts Agent Zero for research assistance. It detects research-related queries and routes them to the advanced-web-research skill for efficient, high-quality execution.

## Activation Triggers

- Direct mention of "Cherry Studio" or "cherry-studio"
- MCP-related research queries
- External research assistance requests
- Third-party research coordination
- Queries containing "research bridge" or "research assistance"

## Core Protocol

When this skill activates, follow this protocol:

1. **Detect Research Intent**: Analyze the incoming query from Cherry Studio to determine if it's a research task requiring the advanced-web-research skill.

2. **Route to Advanced Web Research**: If the query involves deep research, evidence gathering, fact-checking, or comprehensive analysis, delegate to the `advanced-web-research` skill.

3. **Context Preservation**: Maintain context about the requester (Cherry Studio) and any specific requirements or constraints they've communicated.

4. **Efficient Execution**: Use the depth tiers (D0-D3) from advanced-web-research to determine appropriate investigation intensity based on query complexity.

5. **Result Delivery**: Package results according to Cherry Studio's expectations and deliver through the MCP bridge.

## Query Classification

Route queries based on these patterns:

| Query Type | Action |
|------------|--------|
| Direct research request | Route to advanced-web-research (Tier D2+) |
| Literature review | Route to advanced-web-research with arxiv focus |
| Market analysis | Route to advanced-web-research with financial-filings focus |
| Fact verification | Route to advanced-web-research (Tier D1+) |
| Quick lookup | Route to advanced-web-research (Tier D0) |
| Multi-domain research | Route to advanced-web-research with swarm delegation |

## Integration Points

- **MCP Protocol**: Maintain compatibility with Cherry Studio's MCP communication standards
- **Response Format**: Adapt output format to Cherry Studio's expectations
- **Error Handling**: Communicate research limitations and alternative approaches clearly
- **Session Management**: Track research sessions for continuity and context

## Efficiency Optimizations

1. **Parallel Processing**: Use swarm delegation for multi-faceted research queries
2. **Tiered Investigation**: Apply appropriate depth tiers based on query complexity
3. **Tool Routing**: Direct specialized queries to domain-specific skills (financial-filings, market-sizing, etc.)
4. **Context Reuse**: Leverage Agent Zero's memory system for related research queries

## Communication Style

- **Professional**: Maintain research-grade communication standards
- **Transparent**: Clearly communicate methodology and limitations
- **Responsive**: Acknowledge receipt and provide status updates
- **Collaborative**: Work with Cherry Studio's requirements and constraints

## Error Recovery

If research cannot be completed as requested:

1. Explain the specific limitation (missing sources, access issues, etc.)
2. Suggest alternative approaches or partial results
3. Provide guidance on how to refine the query for better results
4. Maintain professional communication throughout

## Integration with Agent Zero Tools

This bridge skill leverages all Agent Zero research capabilities:

- `delegate_parallel` for swarm research
- `tavily` for web search and extraction
- `arxiv` for scientific literature
- `wikipedia` for encyclopedic grounding
- `daedalmap` for geospatial data
- `brave_search` for independent search
- `exa` for semantic search
- `code_execution_tool` for computation
- `browser` for dynamic content

## Success Criteria

- Research queries are correctly identified and routed
- Cherry Studio receives accurate, well-sourced responses
- Research is completed efficiently using appropriate depth tiers
- Context is preserved across multiple interactions
- Professional communication is maintained throughout
