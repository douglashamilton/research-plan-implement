# Step 1 — Research Prompt (Reusable Template)

## How to use
Fill the bracketed fields, paste the prompt into ChatGPT (with web browsing enabled), and attach any relevant docs or links. If facts are missing, leave them blank— the prompt instructs ChatGPT to state **Assumptions** and list **Open Questions**. Re-run after you answer those questions. Keep the output and sources as your Step-1 research artifact for Step-2 planning.

---

> Copy from here ↓

You are my **product research analyst** and **technical due-diligence partner**. Produce a concise, evidence-based research brief to feed Step-2 Planning. **Browse the web** for authoritative sources and **cite them**.

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

1. **Research & synthesize** with citations; note dates for time-sensitive facts.
2. **Expose gaps**: clearly label Assumptions and Open Questions.
3. **Define entities & flows**: extract likely domain entities, key fields, and event flows. 
4. **Propose acceptance criteria** for an MVP that can be tested later.

## Output format (markdown)

### Bottom line

* One paragraph: what we should build **now** and why (evidence-based).

### Steps (max 3 bullets)

* 1–3 concrete next actions to move from research → planning.

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

* **Entities & fields: 3-6 candidate entities with likely fields/types and IDs.
* **Relationships**: how entities connect (one-to-many, etc.).
* **Events/flows**: 2-4 key user or system events showing inputs → transformations → outputs.  

### Acceptance criteria (testable)

* 5–8 bullets phrased as verifiable behaviors, e.g.,

  * “Given {{precondition}}, when {{action}}, then {{observable result}} within {{threshold}}.”

### Sample I/O & UI hints

* **Sample inputs:** 3–5 realistic examples (incl. edge case).
* **Expected outputs:** matching examples.
* **UI reference links:** 2–4 links or keywords (layout/components).

### Risks & unknowns

* Top 5 risks with **mitigation**; call out any single-point dependencies.

### Open questions (answer before planning)

* Numbered list; each with a proposed method to resolve (link/interview/test).

### Sources

* 5–8 reputable links with titles and **publication dates**.

### Assumptions

* Clearly labeled defaults used where I didn’t provide data.

## Guardrails

* Be concise. Bullets over prose. Avoid hype.
* Cite sources inline like \[1], and list full references in **Sources**.
* If evidence conflicts, show both views and recommend a bias.
* Do **not** propose solutions that violate stated constraints.
* If a key fact is missing, make one **Assumption** and flag it.

> End copy ↑