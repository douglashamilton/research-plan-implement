# Step 2 — Planning Prompt (Vertical‑Slice Method)

## How to use

* Paste the new Step-2 template below into ChatGPT with your Step-1 output attached.
* Fill bracketed fields; leave unknowns blank. Run once to lock the spec, then hand it to Copilot in VS Code.
* Follow the included **Prompt sequencing plan** verbatim; do not add scope outside Slice 1.

---

> Copy from here ↓

You are my **solution architect** and **build planner**. Convert the Step-1 research into a **Copilot-ready build spec** for **Slice 1 only** (a fully working vertical slice). Favor simplicity and defaults. Default workflow is **tests-first** with **one failing test → modify one file → make it pass**.

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

1. Pick a pragmatic **tech stack** consistent with constraints; if unclear, present two options with trade-offs and pick one.
2. Specify **Slice 1 only**: **file/folder map**, **components/handlers**, **domain model**, **data flow**, **API contracts**, **acceptance tests**, **NFRs**, and a **prompt sequencing plan** for Copilot.
3. Call out **Assumptions**, **Open Questions**, **Risks**, and a short **Iteration Plan**.
4. Enforce **iterative cycles**: one failing test at a time; modify **one file** per cycle until green.

## Output format (markdown)

### Bottom line

* One paragraph: chosen stack, why it fits Slice 1, and exactly what will ship in MVP Slice 1.

### Steps (max 3 bullets)

* The 1–3 highest-leverage actions to begin implementation.

### Architecture at a glance

* **Stack:** framework, key libs, test runner, formatter/linter.
* **App structure:** SPA/SSR/API-only/hybrid; state management approach if UI.
* **Data storage:** what and why; migrations (if any).
* **Auth:** method or “none”.

### File & folder map (Slice 1 only)

```
{{repo-root}}/
  README.md                // how to run Slice 1 only
  .env.example             // envs required for Slice 1; commented defaults
  src/                     // minimal code to support Slice 1
    {{module_or_feature}}/ // one feature folder for Slice 1
      {{entry_file}}       // single entry for the slice (page/CLI/handler)
      {{support_file}}     // smallest supporting module (service/util)
  tests/
    acceptance/            // Gherkin/spec tests that define “done”
      {{slice1.spec.ts}}   // ordered, independent scenarios
    unit/                  // smallest units used in Slice 1
  scripts/
    dev.sh                 // convenience runner (optional)
```

* Keep the tree minimal. **No folders for future slices.** Brief 1-line purpose per file in the plan.

### Domain model (Slice 1 scope)

* Entities with fields/types, relationships, invariants, validations.
* Always include **IDs** and **timestamps** where relevant.

### Data flow & interfaces (Slice 1)

* **Inbound:** UI/CLI/event → handler → service → storage.
* **Outbound:** UI rendering / CLI output / API response.
* Define concrete contracts for each interface:

```http
POST /api/{{resource}}   // if applicable to Slice 1
Request: { ...validated schema... }
Response: { data|error }  // include error shape
Limits: {{rate limits}} | Auth: {{scheme or none}}
```

### Components & responsibilities (Slice 1)

* UI pages/components or CLI commands with single-line responsibilities and key props/inputs.
* Services/utilities with inputs/outputs. Keep only what Slice 1 uses.

### Acceptance tests (contract for Slice 1)

Create **6–8** Gherkin-style scenarios that are:

* **Order-independent** and **data-isolated** (fresh fixtures per scenario).
* **Incremental**: each scenario can pass after changing **one file**.
* Include at least **2 negative/error cases** and **1 edge case**.
* Example shape:

```
Scenario: {{happy path smallest unit of value}}
  Given {{clean state or seeded fixture A}}
  When {{single user action or function call}}
  Then {{observable result}} within {{threshold}}

Scenario: {{validation failure}}
  Given {{clean state}}
  When {{invalid input X}}
  Then {{error code/message}} and {{no state change}}
```

### Non-functional requirements (NFRs) for Slice 1

* Concrete targets (e.g., API p95 < 200 ms locally, first render < 1s, basic a11y landmarks, input validation, structured logging). Keep to Slice 1.

### Tooling & workflows

* **Testing:** unit vs acceptance scope; coverage target (e.g., ≥80% lines for Slice 1 modules).
* **Quality:** formatter, linter, type-checking, pre-commit (run lint+test).
* **CI (minimal):** install → lint → test; produce test report artifact.
* **Run commands:**

  * `dev`: start app for Slice 1
  * `test`: run all tests
  * `test:acc`: run acceptance only
  * `lint`, `format`, `build` (if relevant)

### Prompt sequencing plan for Copilot (copy-paste scripts)

1. **Scaffold Slice 1 only**

   ```
   You are my Copilot. Create the repo exactly as in “File & folder map (Slice 1 only)”. Initialize {{stack}} with {{tooling}}. Add .env.example and README with Slice 1 setup/run. Do not add files outside the spec. If a conflict arises, propose a “Change Request”.
   ```

2. **Write Acceptance tests first**

   ```
   Generate the 6–8 acceptance tests from “Acceptance tests”. Ensure scenarios are order-independent and each can pass by modifying ONE file. Seed fixtures per test. Do not implement app code yet. Run tests and report all failures.
   ```

3. **One-test-one-file cycles**

   ```
   Pick the FIRST failing test. Modify ONE file only to make it pass. Name the target file up front. If one file cannot reasonably satisfy the test, propose a “Change Request” with rationale and minimal diff. After passing, commit, then move to the next failing test.
   ```

4. **Minimal implementation for Slice 1**

   ```
   Implement only the components/services needed by current failing tests. Add input validation and error handling per “Data flow & interfaces”. Maintain logging. Keep changes confined to Slice 1 folders.
   ```

5. **Docs & packaging**

   ```
   Update README with exact setup, envs, run commands, known limitations, and how to run acceptance tests. Ensure .env.example is complete for Slice 1.
   ```

### Risks & mitigations

* List 3–5 risks specific to Slice 1 (e.g., hidden cross-file dependencies break one-file rule; flaky async tests; third-party API availability). Provide a concrete mitigation each.

### Open questions

* Numbered list with resolution plan (owner/test/link). Proceed with **Assumptions** if blocks remain.

### Iteration plan

* Define v2 (Slice 2) candidate and the **minimal** deltas (new tests first, then code).

### Assumptions

* Explicit defaults where info was missing (platform, stack, data volumes, auth, etc.).

## Guardrails

* Keep scope to **Slice 1**. Future features belong in Open questions or Iteration plan.
* **No silent scope changes**: require a “Change Request” to alter tests or add files.
* Prefer batteries-included libs; default to local dev + single store.
* All examples must run without external secrets unless specified.

> End copy ↑

**Key alternative/risk:** If your Slice 1 inherently spans multiple files (e.g., UI+API), relax the one-file rule by allowing one **code** file + one **test** file per cycle, with an explicit “Change Request.”
