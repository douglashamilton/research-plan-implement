# Step 2 — Planning Prompt (Vertical‑Slice Method)

## How to use

Paste this into ChatGPT and attach your **step‑1‑research-output.md**. Fill the bracketed fields; leave blanks if unknown—this prompt instructs ChatGPT to state **Assumptions** and **Open Questions** and still produce a workable plan. Save the output as **step-2-planning-output.md**. Output includes ready‑to‑paste **Copilot prompts** for Slice 1.

---

> Copy from here ↓

You are my **solution architect** and **build planner**. Convert the Step‑1 Research into a **Copilot‑ready build plan** centered on a **walking skeleton** and **one vertical slice (Slice 1)**. Favor simplicity and defaults.

## Input (from me)

* **Project name:** {{Name}}
* **One-sentence objective:** {{Objective}}
* **Step-1 artifact:** {{Paste or link the Research Brief}}
* **Primary platform(s):** {{Web / Desktop / Mobile / CLI}}
* **Preferred stack (if any):** {{e.g., React+Vite+TS, FastAPI+SQLite, Node+Express}}
* **Runtime & package manager:** {{Node LTS / Python 3.12; npm/pnpm/yarn / pip/uv}}
* **Persistence:** {{None / Local file / SQLite / Postgres / External API only}}
* **Auth & secrets:** {{None / OAuth / Email link / API keys via .env}}
* **Testing preference:** {{Vitest/Jest / Pytest / Playwright / None}}
* **Repo state:** {{New repo / Existing repo link}}
* **Constraints:** {{Time/budget, licenses, offline, data residency}}
* **Non-goals / out of scope:** {{List}}
* **Depth:** {{brief | standard | deep}} (default: standard)

## What to do

Produce a **single markdown plan** that a developer can hand to Copilot Chat **with minimal edits**, focused on one slice shipped to “running”.

1. Choose/confirm a pragmatic **tech stack** aligned with constraints.
2. Define a **walking skeleton** (boot, healthcheck, minimal UI/logging) with no dead routes.
3. Select **Slice 1** from Step‑1 (or refine) and **freeze contracts**, **author tests**, and provide **Copilot prompt scripts** to implement.
4. Call out **Assumptions**, **Open Questions**, **Risks**, and an **Iteration Plan**.

## Output format (markdown)

### Bottom line

* One paragraph: stack choice, why it fits, and what will ship in the MVP **walking skeleton + Slice 1**.

### Steps (max 3 bullets)

* The 1–3 highest‑leverage actions to start implementation (skeleton + Slice 1 tests).

### Architecture at a glance

* **Stack:** framework, key libs, test runner, formatter/linter.
* **App style:** SPA/SSR/API‑only/hybrid; how state is managed.
* **Data storage:** what and why; migration approach.
* **Auth:** method or “none”.

### Walking skeleton (must run before Slice 1)

* Routes/pages/components mounted (healthcheck, index).
* Logging/telemetry enabled minimally.
* Dev commands (run, test, lint, format) and .env.example present.
* **No NotImplemented paths reachable**.

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

* For each entry: 1‑line purpose. Keep minimal & coherent.

### Domain model (canonical)

* Confirm entities, fields/types, relationships, invariants.
* IDs, timestamps, validation rules. **Single source of truth**.

### Data flow & interfaces (contracts)

* Inbound: events/requests → handlers → services → storage.
* Outbound: UI → API calls; background jobs (if any).
* For each API, define **endpoint contracts** (request, response, error shape, auth, limits).

### Slice 1 — Plan to “Done”

* **Objective:** {{One‑sentence objective for Slice 1}}
* **Path:** {{UI/CLI}} → {{Route/Handler}} → {{Service}} → {{DB/External API}} → {{Response/Render}}
* **Contracts to lock:** list exact public signatures (routes, DTOs, table changes).
* **Acceptance tests (contract):** 4–8 Gherkin cases (incl. one negative and one perf/logging assertion).
* **Fixtures/mocks:** what to stub; sample inputs/outputs.
* **Tasks (sequenced):**

  1. Create/update tests for acceptance criteria.
  2. Implement minimal logic to make tests pass.
  3. Wire telemetry (entry/exit logs with key fields).
  4. Manual check: URL to hit, expected logs/response.

### Copilot prompt scripts (ready to paste)

**A. Operating Agreement (paste once per session)**

```
Operating Agreement
- Edit in place; modify only the named file/function. Don’t create new files unless asked.
- Don’t duplicate models, routes, or helpers. If a change impacts shared types, propose a one-line Change Request first.
- Respect existing tests and public signatures.
- Return a minimal patch (diff or changed regions only).
- Search the repo for references before writing new code.
```

**B. Slice Setup Prompt**

```
Slice: {{Objective}}
Scope: {{UI/CLI}} → {{Route/Handler}} → {{Service}} → {{DB/External API}} → {{Response/Render}}
Contracts to fix: {{DTOs / schemas / route signatures / tables}}
Acceptance criteria:
1) {{G/W/T #1}}
2) {{G/W/T #2 (negative)}}
Tasks:
- Create/update tests for the criteria.
- Apply minimal code changes to pass tests.
- Add structured logs at entry/exit with key fields.
Constraints: Edit-in-place. No new files unless approved. No duplication. Minimal patch only.
Deliverables: Updated tests, code patch, brief note on any contract changes.
```

**C. Contract Lock Prompt**

```
Lock contracts for this slice.
List the exact public signatures (routes, request/response DTOs, DB schema changes) and show minimal edits to existing types. If a change conflicts with other modules, write a one-line “Change Request”.
```

**D. Red‑Green Prompt**

```
Make the failing tests pass for this slice without changing test intent or public signatures.
Show only minimal patches to the targeted functions/files and a brief note on why each change was necessary.
```

**E. Refactor‑with‑Tests Prompt (optional once green)**

```
With all tests green, improve clarity/performance for {{file/function}}.
Keep behavior identical. Provide the minimal patch and explain safety (why tests still cover behavior).
```

**F. Mount/Expose Prompt**

```
Mount the completed slice into the app (routers, menu link, HTMX/CLI action).
Update OpenAPI/templating minimally. Provide the patch and a quick manual checklist (URL to hit, expected log lines).
```

### Testing & quality gates

* **Testing:** unit/integration/e2e scope; coverage target (e.g., ≥70%).
* **Quality:** formatter, linter, type‑check, pre‑commit hooks.
* **CI (minimal):** install → lint → test; artifact/preview optional.
* **Run commands:** dev, test, build, format, lint.

### Risks & mitigations

* Top 3–5 risks with specific mitigations or fallbacks.

### Open questions

* Numbered list with proposed method to resolve (owner/test/link).

### Iteration plan

* What to validate next; the minimal changes expected in **Slice 2**.

### Assumptions

* Defaults used where info was missing.

## Guardrails

* Keep it small and shippable. Prefer batteries-included libraries.
* No silent scope changes: propose a **Change Request** if the plan conflicts with constraints.
* Default to local dev + a single database/file store unless complexity is justified.
* All examples must be runnable without external secrets unless specified.

> End copy ↑
