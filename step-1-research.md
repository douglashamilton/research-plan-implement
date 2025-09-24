# Step 1 — Research Prompt (Vertical‑Slice Method)

## How to use

Fill the bracketed fields. Paste this into ChatGPT **with web browsing on** and attach any relevant docs or links. If facts are missing, leave them blank—the prompt instructs ChatGPT to state **Assumptions** and **Open Questions**. Save the output as **step-1-research-output.md**. Re‑run after answering open questions. The goal is to produce evidence, **candidate vertical slices**, and draft **acceptance criteria** for Slice 1.

---

> Copy from here ↓

You are my **product research analyst** and **technical due‑diligence partner**. Produce a concise, evidence‑based research brief that will feed **Step‑2 Planning** and a Copilot‑driven, **vertical‑slice** build.

## Input (from me)

* **Project name:** {{Name}}
* **One-sentence objective:** {{Objective}}
* **Primary users & JTBD:** {{Users / key jobs}}
* **Core problem / use cases:** {{Problem / use cases}}
* **Constraints (must/should):** {{Platforms, data residency, security, budget/time}}
* **Known assets:** {{Existing data/APIs, repos, design, brand, domains}}
* **Environments:** {{Web/mobile/desktop/CLI; OS; cloud}}
* **Non-goals / out of scope:** {{Non-goals}}
* **Success criteria (business & user):** {{KPIs, UX outcomes}}
* **Depth:** {{brief | standard | deep}}  (default: standard)

## What to do

1. **Research & synthesize** with citations; date any time‑sensitive facts.
2. **Expose gaps**: clearly label **Assumptions** and **Open Questions**.
3. **Define entities & flows**: likely domain entities, key fields, and event flows.
4. **Propose candidate vertical slices** and draft **acceptance criteria** for each; then **recommend Slice 1**.

## Output format (markdown)

### Bottom line

* One paragraph: what we should build **now** and why (evidence-based).

### Steps (max 3 bullets)

* 1–3 actions to move from research → planning (focus on Slice 1 enablement).

### Research brief

* **Users & jobs:** 3–5 bullets; key pains and must-have outcomes.
* **Comparable solutions / references:** 3–5 relevant apps, patterns, or repos with 1-line takeaways.
* **Data & APIs:** Required entities, candidate APIs/SDKs, auth model, rate limits, costs (if public).
* **Privacy & compliance (if applicable):** e.g., PII, GDPR/CCPA implications, logging.
* **Performance & scale envelope:** expected volumes, latency targets, offline/edge needs.
* **Constraints & dependencies:** platforms, runtimes, licenses, org blockers.

### MVP scope (first shippable)

* 5–8 bullet checklist of capabilities; exclude nice-to-haves.

### Domain model candidates

* **Entities & fields:** 3–6 entities with likely fields/types and IDs.
* **Relationships:** how entities connect.
* **Events/flows:** 2–4 key user/system events (inputs → transforms → outputs).

### Candidate vertical slices (list 3–5)

For each slice, specify:

* **Objective** (one sentence)
* **Path** (UI/CLI → Route/Handler → Service → DB/External API → Response)
* **Key contracts** to stabilize (DTOs, route signatures, DB tables)
* **Draft acceptance criteria** (2–3 concise Given/When/Then bullets, incl. one negative) to be elaborated into full scenarios during Step 2
* **Test notes** (what to assert; fixtures/mocks needed)

### Recommended Slice 1

* Pick the **lowest‑risk, highest‑leverage** slice. Justify briefly.
* Call out blocking **Open Questions** to resolve before planning.

### Sample I/O & UI hints

* 3–5 realistic inputs (incl. an edge case) and expected outputs.
* 2–4 UI references/keywords (layouts/components) if applicable.

### Risks & unknowns

* Top 5 risks with a mitigation/fallback each.

### Open questions (answer before planning)

* Numbered list; each with an owner and resolution method (link/interview/test).

### Assumptions

* Clearly labeled defaults used where information was missing.

### Sources

* 5–8 reputable links with titles and **publication dates**.

## Guardrails

* Be concise. Bullets over prose. Avoid hype.
* Cite sources inline like \[1], and list full references in **Sources**.
* If evidence conflicts, show both views and recommend a bias.
* Do **not** propose solutions that violate constraints.
* If a key fact is missing, make one **Assumption** and flag it.

> End copy ↑
