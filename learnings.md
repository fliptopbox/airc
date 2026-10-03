# AI Adoption Retrospective: The Good, The Bad, and The Ugly

> **Date:** September 19, 2026
> **Scope:** Analysis of AI tool harnesses, agent directives, and prompt engineering across the `lifedrawing.art` repository.

## Executive Summary
This project represents a fascinating evolution from a traditional solo-developer codebase into an **agent-orchestrated workspace**. You are no longer just writing code; you are acting as an engineering manager for a team of LLMs. You have successfully implemented advanced patterns like context-injection via global directives and custom skill definitions. 

However, this transition has brought significant overhead. The repository is heavily fragmented across multiple AI ecosystems, leading to configuration sprawl, context synchronization friction, and occasional pipeline failures caused by agent hallucinations.

Here is an honest breakdown of how AI is being utilized in this project.

---

## 🟢 The Good: Advanced Orchestration & Boundary Setting

### 1. Masterful Context Management
Most developers fail with AI because they rely on the chat window's context window. You have solved this by creating persistent, repository-level state machines:
- **`SYSTEM_DIRECTIVE_GLOBAL.md`**: Sets the architectural north star.
- **`docs/database/plan.md`**: Acts as a kanban board where agents mark tasks as `✅ DONE` or `🔄 IN PROGRESS`. This allows a new agent to spin up, read the file, and resume a complex 40-step database migration exactly where the last agent left off.

### 2. Strict Security Guardrails
Your `AGENT_GUARDRAILS.md` is a masterclass in preventing AI-driven security disasters. By explicitly defining the "Service-Role Isolation Boundary" and dictating exact `SELECT` statements for public data, you are actively preventing agents from inadvertently exposing PII (like model phone numbers) during automated refactors.

### 3. Specialized Custom Skills (Antigravity)
Rather than relying on generic LLM knowledge, you've built a robust `.agents/skills/` directory. 
- You recognize that LLM training data is often outdated, so you built a `modern-web-guidance` skill to force the AI to use new CSS features.
- You built `fzfast` (a token-efficient python refactor script) to overcome context window limits during large-scale file edits.
- You built `grill-me` to force the AI to interview you and challenge your assumptions before writing code.

---

## 🟡 The Bad: Tool Sprawl & Maintenance Overhead

### 1. Ecosystem Fragmentation
You are suffering from severe **AI Tool Fatigue**. A scan of the root directory reveals configurations for:
- **Antigravity (AGY)** (`.agents/`)
- **Claude Code** (`.claude/settings.local.json`)
- **GitHub Copilot** (`.github/copilot-instructions.md`)
- **n8n + Gemini** (Live product chatbot)

You are paying the mental tax of context-switching between different agent harnesses, each with its own quirks, permission models (e.g., Claude's Bash allowlist vs. AGY's MCP integration), and configuration syntax. 

### 2. The Maintenance Burden of Prompts
Your `AGENT_TASK_PROMPTS.md` contains highly specific, procedural prompts (e.g., "Write a standalone Node.js migration script... Use `@supabase/supabase-js`"). While effective, these prompts are deeply coupled to the current state of the codebase. If the architecture shifts, maintaining these prompt libraries becomes as burdensome as maintaining legacy code.

### 3. Manual State Synchronization Friction
Relying on agents to read and update `docs/database/plan.md` is clever, but fragile. If an agent hallucinates, crashes (due to rate limits), or simply forgets to check off a box, the state file becomes corrupted. The next agent entering the workspace will read stale data and step on the previous agent's toes.

---

## 🔴 The Ugly: Hallucinations Breaking the Pipeline

### 1. CI/CD Crashes via AI Hallucination
The commit history reveals a dark side to automated documentation generation:
> `06af231c fix(docs): redact URL from guardrails to actually pass the scanner`
> `4b9b870d docs(guardrails): strictly prohibit hardcoding live urls in markdown to prevent secret scanner crashes`

An AI agent, while writing documentation, hallucinated or hardcoded a live Supabase URL/secret into a markdown file. This triggered Netlify/GitHub secret scanners and crashed the build pipeline. You had to implement a specific guardrail just to stop the AI from self-sabotaging the CI process.

### 2. Over-Engineering Simple Solutions
The `fzfast` skill is a prime example of AI-induced over-engineering. Maintaining 6 custom Python scripts (`ast_scan.py`, `rank_candidates.py`, etc.) just to pre-warm and rank files for an LLM is a massive abstraction leak. You are maintaining complex code whose sole purpose is to make another tool work properly. 

---

## 💡 Recommendations for the Next Phase

1. **Consolidate the Harness:** Pick one primary agentic IDE (Antigravity seems to be your most mature setup) and deprecate the localized `.claude` and `.github/copilot` configurations. Unify your instructions under one engine.
2. **Shift from "Plan Files" to "Agent Memory":** Instead of forcing agents to edit `plan.md` using string replacement, explore using MCP (Model Context Protocol) servers that allow the agent to interface directly with a real Kanban board (like Linear or GitHub Projects) via API. It is far less error-prone than parsing markdown tables.
3. **Embrace the "Rubber Duck" Paradigm:** Your `grill-me` skill is the most powerful tool in your arsenal. Rely less on AI as a "junior dev typing out code" and more as a "senior architect challenging your design." 

You have successfully crossed the chasm from writing code to orchestrating systems. The next challenge is simplifying the orchestration layer before the management overhead outweighs the productivity gains.
