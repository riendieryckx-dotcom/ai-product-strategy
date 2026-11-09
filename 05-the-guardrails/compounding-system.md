# Compounding System Design

## Feedback Loops

| Loop | Input | Output | Compounds? | Status |
|------|-------|--------|-----------|--------|
| Implicit use | Findings that physicians take over into notes and letters, and sources they open; no extra click | A better selection of findings in the EHR software for all hospitals, updated weekly (pooled across hospitals once each hospital has given a legal basis; until then per hospital) | Y | missing — reading the notes after display is not built |
| Confirmed outcomes | Diagnoses confirmed at discharge or when a consultation is closed, plus physicians' marks | Weekly recalibration of likelihood and severity per hospital, within preset limits | Y | broken — simulated in the prototype; no pipeline |
| Missed cases to eval | Missed diagnoses found in review: not in the list, severity 3–4, or an unplanned admission within 30 days | New golden rows and must-not-miss checks that every release must pass | Y | missing — the review triggers exist; the loop does not |

**Broken loop identified by partner:** to fill in after the peer challenge (draft: confirmed outcomes, because marks and confirmations never leave the page).
**Fix plan:** in the pilot, build the implicit-use loop first, because it gives a signal on every stay without extra clicks; then ship the confirmation click and store marks in the audit log. Measure the share of signals that reaches the weekly update. Freeze test: today the product would still win after 3 months, so it scales; it compounds only once these loops run. Once they run, a 3-month freeze would visibly degrade the selection of findings (implicit use) and the calibration (confirmed outcomes).

## Context Connectivity

Discharge codes never flow back to the physician, outpatient diagnoses are not coded, and the vendor's review findings reach hospitals only once a quarter. Reading the notes after a finding was shown is a new purpose for health data; to confirm with legal and the DPO.

## Governance Policy

**Scope:** Relevant History in internal medicine, in stays and outpatient workups; not the prototype or other AI in the EHR.
**Autonomy boundaries:** read, select, draft and show: auto. Write to the record: never. Recalibrate: weekly, within preset limits, after the golden suite passes. Change the model: never auto.
**Escalation triggers:** low confidence, a safety flag, a rejected high-severity suggestion, a missed serious case, a subgroup or drift alert, a suspected incident (details in `04-the-contract/golden-dataset.md`).
**Audit cadence:** real time (engineering), weekly (product owner), monthly (lead of the clinical team), quarterly with regulatory, security, legal and the DPO (sign-off: clinical safety officer). Maturity: Level 2 today (golden set, confidence tiers, reliability contract); Level 3 with a model card and a public bias posture backed by the subgroup reports.
**Regulatory exposure (EU AI Act / other):** AI Act high risk; MDR likely class IIb; GDPR article 9, with the hospital as controller, the vendor as processor and Google as sub-processor; Belgian eHealth law. To confirm with regulatory, legal and the DPO.

## Agent Topology

Two models behind a rule-based gateway; not an autonomous agent.

- **Triage model (Gemini Flash-class):** reads one patient's record and selects findings. No writes, no tools, no memory.
- **Suggestion model (Gemini Pro-class):** writes suggestions from the selected findings only. No writes, no memory.
- **Gateway:** checks every claim against the record, blocks tests, treatments and doses, and stops the chain on a failed check. Owners: engineering for the handoff, the clinical safety officer for the content.
- **Tool calls:** the models call no tools. Every model call is logged with its reason and result, with a rate limit per hospital.
- **Memory:** short-term per request only; no long-term memory per patient; shared across hospitals only as aggregated calibration, with a legal basis.
- **Approvals:** the physician for every use of a suggestion; the clinical safety officer for any release outside the limits.

## Shadow AI Audit

| Tool | Owner | Risk Level | Decision |
|------|-------|-----------|----------|
| Physicians paste record extracts into a general chatbot for a differential (capability gap) | Interviews | H | build — this is the product; also a GDPR risk to raise with the hospital's CISO |
| Physicians ask a chatbot to summarise long letters from other hospitals (workflow gap) | Interviews | H | build — a workflow gap usually means partner, but summarising the history is the core of this product |
| Physicians ask a chatbot to translate letters in French or German (capability gap) | Interviews | M | build — part of the findings layer, which already reads other languages |
| Physicians check a guideline platform next to a suggestion (trust gap) | Interviews | M | partner — link suggestions to guidelines; revisit the confidence UX |
| Physicians ask an ambient documentation assistant for a differential (workflow gap) | Hospital IT | M | partner — make the module callable from the assistant |

**Total tools found:** 5 workarounds, all hypotheses to verify in tickets, interviews and with hospital IT.
**Tools after triage:** 3 build, 2 partner.
**Estimated hidden spend:** [€__ per hospital per month], to measure.
