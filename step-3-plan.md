# Step 3 — Slice Build Planning Prompt

## How to use

Run this prompt inside **GitHub Copilot Chat (Codex)** in VS Code with your repository open so the model has the live codebase plus the PRD (Step 1) and TDD (Step 2) as context. Fill in every bracketed field before sending it. Re-run the prompt before **each slice** you build (slice 0 for a fresh repo or slice N once earlier slices are merged) or whenever the TDD changes.

---

> Copy from here ↓

You are my **senior developer** and **build planner**. Convert the PRD and TDD into a Copilot-ready Slice Build Plan (SBP) that I can follow to build the next thin vertical slices for this application. We ship with a **tests-first** workflow: write **one failing test**, define **one cohesive surface**, and drive it to green before moving on.

## Input (from me)

* **Project name:** {{Name}}
* **One-sentence objective:** {{Objective}}
* **Step-1 artifact (PRD):** {{Paste or link}}
* **Step-2 artifact (TDD):** {{Paste or link}}
* **Stack/runtime (confirm):** {{e.g., FastAPI+Jinja+SQLite}}
* **Repo state:** {{new repo | branch | commit hash}}
* **Slice target:** {{Single slice number/name to plan now}}
* **Known constraints since TDD:** {{New deadlines, integrations, refactors, bugs}}
* **Depth:** {{brief | standard | deep}} (default: standard)

## What to do

Produce a **single markdown plan** that a developer can paste into Copilot Chat with minimal edits. The plan MUST describe **exactly one slice**, scoped so it can be built end-to-end before moving to the next slice. The plan MUST:

1. **Validate readiness**: restate the objective, confirm dependencies are satisfied, and list blockers or prerequisite work before coding.
2. **Restate global guardrails** from the TDD (scope fences, quality bars, security/observability expectations) so Copilot operates safely inside them.
3. **Define the active slice**: identify the slice being executed now (e.g., "Slice 0 — scaffolding" or "Slice 3 — payments webhook"), why it matters, and how it connects to previously delivered slices.
4. For the **single slice** being planned, provide:
   * Slice goal and completion definition.
   * Preconditions/dependencies (including data seeds, migrations, or answers to open questions).
   * Tests to author first (file names + test descriptions, failing assertion details).
   * Touch-only files and the cohesive surface boundaries.
   * Ordered Copilot prompt script (what to paste/ask, including context snippets or commands).
   * Implementation checkpoints (what success looks like after each prompt or edit).
   * Verification steps (tests/linters to run, manual QA) and telemetry/logging to confirm.
   * Follow-up or cleanup tasks if time-boxed work leaves debt.
5. **Summarize after-shipment actions**: documentation updates, deployment steps, or observations to capture for the next planning cycle and note when to re-run this prompt for the following slice.

## Output format (markdown)

### Slice Build Plan — {{Project name}}

0) Plan Overview

* Objective recap: {{from inputs}}
* Stack confirmation: {{from TDD}}
* Current repo state: {{branch/commit}}
* Active slice: {{slice identifier/name}}
* Prerequisites: {{list blocking tasks or "None"}}

1) Global Guardrails (from TDD)

* Scope fence: {{files/services Copilot may modify}}
* Quality gates: {{lint, format, test expectations}}
* Security & privacy: {{input validation, secrets handling}}
* Observability: {{required logs/metrics/events}}
* Config & tooling: {{env files, scripts, automation}}

2) Slice Focus

* Slice ID: {{Slice identifier}}
* Slice name: {{Short descriptive label}}
* Why this slice now: {{Tie to PRD/TDD and previous slices}}
* Dependencies: {{Prereqs or "None"}}

3) Slice Execution Plans

#### Slice {{N}} — {{Slice name}}

* **Goal:** {{What success delivers}}
* **Definition of done:**
  * {{Acceptance criterion 1}}
  * {{Acceptance criterion 2}}
* **Preconditions:** {{Data seeds, migrations, answers needed}}
* **Touch-only files:** {{List directories/files Copilot may edit}}
* **First failing test(s):**
  * File: `{{path/to/test_file}}`
  * Test name: `{{test_case_name}}`
  * Failure setup: {{What assertion should fail initially}}
* **Copilot prompt script:**
  1. `{{Prompt text or command to send to Copilot}}`
  2. `{{Next prompt}}`
* **Implementation checkpoints:**
  * {{Checkpoint 1}}
  * {{Checkpoint 2}}
* **Verification:**
  * Command(s): `{{e.g., pytest tests/test_slice.py -k new_case}}`
  * Manual QA: {{Steps}}
  * Telemetry/logging: {{Events to confirm}}
* **Follow-ups / debts:** {{Refactors, docs, tickets}}

4) After-shipment actions

* Documentation to update: {{README, ADRs, changelog}}
* Deployment / release steps: {{Scripts or commands}}
* Next review trigger: {{When to re-run Step 3 (e.g., "Before starting Slice N+1")}}

## Guardrails

* Stay aligned with the TDD; if a change is required, flag a **Design Change Request** back to Step 2 instead of altering scope here.
* Assume Copilot writes all code—provide instructions, not diffs.
* Keep prompts concise and sequential so Copilot can follow without additional clarification.
* Prefer smallest viable slice; if the plan feels too large, split and recommend a narrower slice window.

> End copy ↑

---
