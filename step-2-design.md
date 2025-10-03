# Step 2 — Design Prompt

## How to use

Paste the new Step-2 template below into ChatGPT with your Step-1 output attached. Fill bracketed fields; leave unknowns blank. Run once to lock the design that Step 3 will turn into a slice-by-slice plan.

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
2. Describe the end-to-end **system architecture**: **file/folder map**, **modules/components**, **data model**, **data flow**, and **interface contracts** that will support the entire MVP scope defined in Step 1.
3. Capture **acceptance criteria** for the overall solution, cross-cutting **non-functional requirements**, and the engineering guardrails Copilot must respect when generating code.
4. Call out **Assumptions**, **Open Questions**, **Risks**, and an **Iteration Readiness Checklist** that confirms the design is ready for Step 3 slice planning.

## Output format (markdown)

### Bottom line

* One paragraph: exactly what will be shipped in the MVP and the chosen stack, highlighting the primary capabilities the architecture must support (no slice planning yet).

### Architecture Overview

* **Stack:** framework, key libs, test runner, formatter/linter.
* **App structure:** SPA/SSR/API-only/hybrid; state management approach if UI.
* **Data storage:** what and why; migrations (if any).
* **Auth:** method or “none”.
* **Deployment & environments:** local dev workflow, CI/CD or manual deploy expectations.

### Tech Stack Decisions

* Detail the recommended language/runtime, frameworks, databases and key libraries, with rationale and key configuration decisions.

### Interfaces

* Detail the necessary API contracts, module contracts and event / telemetry contracts (as applicable).
* Include inputs/outputs, validation rules, and error handling strategy.

### Domain model

* Entities with fields/types, relationships, invariants, validations.
* Always include **IDs** and **timestamps** where relevant.
* Note persistence choices (e.g., tables, collections) and indexing considerations.

### Data flow & interfaces

* **Inbound:** UI/CLI/event → handler → service → storage.
* **Outbound:** UI rendering / CLI output / API response.
* Define concrete contracts for each interface:

```http
POST /api/{{resource}}   // if applicable to the MVP scope
Request: { ...validated schema... }
Response: { data|error }  // include error shape
Limits: {{rate limits}} | Auth: {{scheme or none}}
```

### Tooling & workflows

* **Testing:** unit vs acceptance scope; coverage target and types of automated tests honoring mandated tooling from Step-1 constraints.
* **Quality:** formatter, linter, type-checking, pre-commit (run lint+test) consistent with Step-1 engineering standards.
* **Collaboration:** branching strategy, code review expectations, docs to update.

### Risks & mitigations

* List 3–5 risks. Provide a concrete mitigation for each.
* Flag any design decisions that require validation with stakeholders.

### Assumptions

* Explicit defaults where info was missing (platform, stack, data volumes, auth, etc.).

### Open questions

* Numbered list with resolution plan (owner/test/link). Proceed with **Assumptions** if blocks remain.

### Iteration readiness checklist

* Bullet list confirming the design gives Step 3 everything required: bounded MVP scope, clear contracts, defined dependencies, and any pre-work needed before slicing.

## Guardrails

* Keep scope at the **system design level**. Do not create slice-by-slice execution plans (that is Step 3’s responsibility).
* **No silent scope changes**: require a “Change Request” to alter tests or add files.
* Prefer batteries-included libs; default to local dev + single store.
* All examples must run without external secrets unless specified.

> End copy ↑

----
