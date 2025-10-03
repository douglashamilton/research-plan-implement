# Step 2 — Design Prompt

## How to use

Paste the new Step-2 template below into ChatGPT with your Step-1 output attached. Fill bracketed fields; leave unknowns blank. Run once to lock the design, then hand it to Copilot in VS Code. 

---

> Copy from here ↓

You are my **solution architect**. Convert the Step-1 research (PRD) into a **Copilot-ready Technical Design Document (TDD)**. Favor simplicity over complexity. 

## Input (from me)

* **Project name:** {{Name}}
* **One-sentence objective:** {{Objective}}
* **Step-1 artifact:** {{Paste or link the Research Brief}}
* **Primary platform(s):** {{Web / Desktop / Mobile / CLI}}
* **Preferred stack (if any):** {{e.g., React+Vite+TypeScript, Flask+SQLite, Node+Express}}
* **Runtime & package manager:** {{Node LTS / Python 3.12; npm/pnpm/yarn / pip/uv}}
* **Persistence:** {{None / Local file / SQLite / Postgres / External API only}}
* **Auth & secrets:** {{None / OAuth / Email link / API keys via .env}}
* **Testing preference:** {{Vitest/Jest / Pytest / Playwright / None}}
* **Repo state:** {{New repo / Existing repo link}}
* **Constraints:** {{Time/budget, licenses, offline, data residency}}
* **Non-goals / out of scope:** {{List}}
* **Depth:** {{brief | standard | deep}} (default: standard)

## What to do

Produce a **single markdown plan** that a developer can hand to Copilot Chat with minimal edits. The plan MUST:

1. Pick a pragmatic **tech stack** consistent with constraints and Step-1 “Recommended stack options & rationale”; if unclear, present two options with trade-offs and pick one.
2. Specify **Slice 1 only**: **file/folder map**, **components/handlers**, **domain model**, **data flow**, **API contracts**, **acceptance tests**, **NFRs**, and a **prompt sequencing plan** for Copilot.
3. Call out **Assumptions**, **Open Questions**, **Risks**, and a short **Iteration Plan**.
4. Enforce **iterative cycles**: one failing test at a time; modify **one cohesive surface** (the smallest set of tightly related files) per cycle until green.

## Output format (markdown)

### Bottom line

* One paragraph: exactly what will be shipped in the MVP, the chosen stack, and a breakdown of each vertical slice (in order of implementation). 

### Architecture Overview

* **Stack:** framework, key libs, test runner, formatter/linter.
* **App structure:** SPA/SSR/API-only/hybrid; state management approach if UI.
* **Data storage:** what and why; migrations (if any).
* **Auth:** method or “none”.

### Tech Stack Decisions

* Detail the recommended language/runtime, frameworks, databases and key libraries. 

### Interfaces

* Detail the necessary API contracts, module contracts and event / telemetry contracts (as applicable).

### Domain model

* Entities with fields/types, relationships, invariants, validations.
* Always include **IDs** and **timestamps** where relevant.

### Data flow & interfaces

* **Inbound:** UI/CLI/event → handler → service → storage.
* **Outbound:** UI rendering / CLI output / API response.
* Define concrete contracts for each interface:

```http
POST /api/{{resource}}   // if applicable to Slice 1
Request: { ...validated schema... }
Response: { data|error }  // include error shape
Limits: {{rate limits}} | Auth: {{scheme or none}}
```

### Tooling & workflows

* **Testing:** unit vs acceptance scope; coverage target (e.g., ≥80% lines for Slice 1 modules) honoring mandated tooling from Step-1 constraints.
* **Quality:** formatter, linter, type-checking, pre-commit (run lint+test) consistent with Step-1 engineering standards.

### Risks & mitigations

* List 3–5 risks. Provide a concrete mitigation for each.

### Assumptions

* Explicit defaults where info was missing (platform, stack, data volumes, auth, etc.).

### Open questions

* Numbered list with resolution plan (owner/test/link). Proceed with **Assumptions** if blocks remain.

## Guardrails

* Keep scope to **Slice 1**. Future features belong in Open questions or Iteration plan.
* **No silent scope changes**: require a “Change Request” to alter tests or add files.
* Prefer batteries-included libs; default to local dev + single store.
* All examples must run without external secrets unless specified.

> End copy ↑

----
