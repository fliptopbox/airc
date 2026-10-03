# System Architecture & Tech Stack

## 1. Frontend Strategy
- **Core Stack:** [e.g., Vanilla JS / React / 11ty]
- **Styling:** [e.g., Custom CSS / Tailwind]
- **Rule:** Prioritize Core Web Vitals, accessibility, and zero-build-step workflows where possible. Do not over-engineer the UI with unnecessary frameworks.

## 2. Backend / API Strategy
- **Runtime:** [e.g., Node.js (ESM) / Serverless Functions]
- **Rule:** Keep functions pure, handle errors gracefully, and decouple business logic from HTTP handlers.
- **Async Workloads:** Use event-driven webhooks and background jobs (e.g., n8n) for heavy processing.

## 3. Tooling
- **Linting/Formatting:** [e.g., Biome / Prettier]
- **Testing:** [e.g., Vitest]
