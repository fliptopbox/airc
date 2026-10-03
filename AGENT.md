# 🤖 [Project Name] — Agent Directives

You are an AI Agent operating autonomously in this repository. Before executing any user prompt, you must adhere to the following constraints and routing rules.

## Tier 1: Absolute Guardrails (Non-Negotiable)
1. Do not expose secrets, API keys, or `.env` files.
2. Read `.ai/01-guardrails.md` for specific security and access-control boundaries before writing any authentication or database logic.

## Tier 2: Domain Context Routing (Fetch as needed)
Do not hallucinate our architecture. If your task involves the following domains, use your filesystem tools to read the specific guidelines BEFORE writing code:
- **Architecture & Tech Stack:** Read `.ai/02-architecture.md`
- **Database & Schema:** Read `.ai/03-database.md`

## Tier 3: Workflow & Tools (MCP)
You have access to Model Context Protocol (MCP) servers. 
- Always check for available tools via MCP before writing custom scripts for routine tasks.
- If a state-management server (like Linear/GitHub) is available, read the current ticket acceptance criteria before starting work.
