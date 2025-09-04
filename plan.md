# Step 2 — Planning Prompt (Reusable Template)

## How to use

Paste this into ChatGPT and attach your Step-1 Research output. Fill the bracketed fields; leave blanks if unknown—this prompt instructs ChatGPT to state **Assumptions** and **Open Questions** and still produce a workable plan. Expect 1–2 iterations to lock the spec before handing it to Copilot in VS Code.

---

> Copy from here ↓

You are my **solution architect** and **build planner**. Convert the Step-1 Research Brief into a **Copilot-ready build spec** for a basic–medium complexity app. Favor simplicity and defaults.

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

Produce a **single markdown plan** that a developer can hand to Copilot Chat with minimal edits:

1. Pick a pragmatic **tech stack** consistent with constraints; if unclear, present two options with trade-offs and pick one.
2. Specify **file/folder map**, **components**, **domain model**, **data flow**, **API contracts**, **acceptance tests**, **NFRs**, and a **prompt sequencing plan** for Copilot.
3. Call out **Assumptions**, **Open Questions**, **Risks**, and a short **Iteration Plan** to close gaps.

## Output format (markdown)

### Bottom line

* One paragraph: stack choice, why it fits, and what will ship in MVP.

### Steps (max 3 bullets)

* The 1–3 highest-leverage actions to move into implementation.

### Architecture at a glance

* **Stack:** framework, key libs, test runner, formatter/linter.
* **App structure:** SPA/SSR/API-only/hybrid; how state is managed.
* **Data storage:** what and why; migration approach (if any).
* **Auth:** method or “none”.

### File & folder map (initial)

```
{{project-root}}/
  README.md
  .env.example
  {{src or app}}/
    {{modules/components/...}}
  tests/
  scripts/
```

* For each entry: 1-line purpose. Keep tree minimal and coherent.

### Domain model

* Refine the **Domain modal candidates** from Step-1 into a confirmed set of entities.
* Entities with fields/types, relationships, and invariants (bulleted).
* Include **IDs**, **timestamps**, and validation rules.

### Data flow & interfaces

* Refine Step-1 **Events/flows** into concrete inbound/outbound data flows. 
* **Inbound:** events/requests → handlers → services → storage.
* **Outbound:** UI → API calls; background jobs (if any).
* For each API (internal/external), define **endpoints/contracts**:

```http
POST /api/{{resource}}
Request: { ... }
Response: { ... }  // include error shape
Limits: {{rate limits}} | Auth: {{scheme}}
```

### Components & responsibilities

* UI components / pages (or CLI commands) with 1-line responsibilities and key props/inputs.
* Services/utilities with inputs/outputs.

### Acceptance tests (contract)

* 6–10 Gherkin-style cases that **define done**:

```
Scenario: {{feature}}
  Given {{precondition}}
  When {{action}}
  Then {{observable result within threshold}}
```

### Non-functional requirements (NFRs)

* Performance targets (latency, throughput), reliability, accessibility, i18n, logging/telemetry, security basics. Include concrete numbers when possible.

### Tooling & workflows

* **Testing:** unit/integration/e2e scope; coverage target.
* **Quality:** formatter, linter, type-checking, pre-commit hooks.
* **CI (minimal):** install → lint → test; artifact or preview step.
* **Run commands:** dev, test, build, format, lint.

### Prompt sequencing plan for Copilot (copy-paste scripts)

1. **Scaffold & config**

   ```
   You are my Copilot. Create the repo structure exactly as per the “File & folder map”. Initialize {{stack}} with {{tooling}}. Add .env.example and README skeleton. Do not invent files outside the spec. If a conflict arises, propose a Change Request.
   ```
2. **Domain & contracts**

   ```
   Generate types/models and validation per “Domain model”. Create API routes and request/response schemas from “Data flow & interfaces”. Add error handling and tests.
   ```
3. **UI/CLI implementation**

   ```
   Build components/pages listed in “Components & responsibilities”, using placeholder styling. Wire to APIs. Add loading/empty/error states.
   ```
4. **Acceptance tests first**

   ```
   Create test files implementing all “Acceptance tests”. Run tests; report failures.
   ```
5. **Make tests pass**

   ```
   Implement missing logic until all acceptance tests pass. Do not change test intent without a Change Request.
   ```
6. **Docs & packaging**

   ```
   Fill README with setup/run instructions, env vars, and limitations. Generate .env.example values and comments.
   ```

### Risks & mitigations

* Top 3–5 risks with specific mitigations or fallbacks.

### Open questions

* Numbered list with proposed method to resolve (owner/test/link).

### Iteration plan

* What to validate next, and the minimal changes expected in v2.

### Assumptions

* Clearly labeled defaults used where info was missing.

## Guardrails

* Keep it small and shippable. Prefer batteries-included libraries.
* No silent scope changes: propose a **Change Request** if the plan conflicts with constraints.
* Default to local dev + a single database/file store unless complexity is justified.
* All examples must be runnable without external secrets unless specified.

> End copy ↑