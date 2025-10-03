# Step 3 - Planning Prompt

## How to use

Paste the PRD (Step 1 artifact) and the TDD (Step 2 artifact) into ChatGPT as attachments. Fill the bracketed fields detailing the slice that needs to be planned. Run this prompt and apply the instructions in Copilot in VS Code. 

---

> Copy from here ↓

You are my **senior developer** and **build planner**. Convert the TDD and the PRD into a copilot ready build plan that can be followed by me to build the next thin vertical slice for my application. The vertical-slice workflow is **tests-first** with **one failing test → declare one cohesive surface → make it pass**.

## Input (from me)
* **Project name:** {{Name}}
* **One-sentence objective:** {{Objective}}
* **Step-1 artifact:** {{Paste or link the PRD}}
* **Step-1 artifact:** {{Paste or link the TDD}}
* **Stack/runtime:** {{e.g., FastAPI+Jinja+SQLite | Streamlit+SQLite | other as per TDD}}
* **Repo state:** {{new repo | link}}
* **Depth:** {{brief | standard | deep}} (default: standard)

## What to do

Produce a **single markdown plan** that a developer can hand to Copilot Chat with minimal edits. The plan MUST:

1. Define 

## Output format (markdown)

### Slice Plan — {{Project name}}

0) Plan Overview:

* Stack: {{from TDD}}
* Current codebase state: {{commit/tag or “new repo”}}
* Window: slices planned now = {{Slice 0..2}} (re-plan after each shipment)
* Policy: TDD contracts are frozen during this window; any change requires a TDD change first (Step-2) and then slice regeneration.

1) Global Guardrails (from TDD):

* Scope fence: Copilot may only modify files in each slice’s Touch-only list.
* Quality gates: lint/format/test must pass; structured logs emit required events.
* Security: input validation, secrets via .env, no PII in logs.
* Observability: log {ts, level, event, request_id}; emit events listed per slice.
* Config: local-first run; .env.example maintained.