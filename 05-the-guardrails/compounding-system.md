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

**Scope:**
- **In:** Relevant History in internal medicine, during hospital stays and outpatient workups.
- **Out:** the prototype on synthetic data, and other AI features in the EHR, which have their own policies.

**Autonomy boundaries:**

| Action | Autonomy |
|--------|----------|
| Read the patient's record, select findings, draft and show suggestions | Automatic |
| Write anything to the record (a diagnosis, a code, a problem-list entry, an order, a message to a patient) | Never by the module; only the physician |
| Recalibrate likelihood and severity | Automatic, weekly, within preset limits, and only after the golden suite passes |
| Release a change outside those limits | Only with approval of the clinical safety officer |
| Change the model or the model version | Never automatic; only through a validated release |

**Escalation triggers:** a human reviews the case when:
1. confidence is low (below 70%);
2. the gateway raises a safety flag (a claim not in the record, or a test, treatment or dose);
3. a physician rejects a suggestion with a severity of 40% or more;
4. a serious case was missed: a confirmed diagnosis that was not in the list during a severity 3–4 stay, or an unplanned admission within 30 days of an outpatient workup;
5. a subgroup or drift alert fires;
6. a serious incident is suspected, which also starts vigilance.

Thresholds and details: `04-the-contract/golden-dataset.md`.

**Audit cadence:**

| Cadence | What is checked | Owner |
|---------|-----------------|-------|
| Real time | Grounding check on every output | Engineering (on-call) |
| Weekly | Golden suite, judge run and the recalibration gate | Product owner |
| Monthly | Accuracy and tier calibration per hospital; the review sample | Lead of the clinical team |
| Quarterly | Subgroups, independent reference, hospital reports, and a policy review with regulatory, security, legal and the DPO | Clinical safety officer (sign-off) |

Maturity: Level 2 today (golden set, confidence tiers, reliability contract). Target Level 3: a model card and a public bias posture, backed by the subgroup reports.

**Regulatory exposure (EU AI Act / other):**

| Framework | Exposure |
|-----------|----------|
| EU AI Act | High risk: an AI system in a medical device that needs a notified body |
| MDR | Likely class IIb; serious incidents reported within 2, 10 or 15 calendar days |
| GDPR | Article 9 health data; the hospital is controller, the vendor processor, Google sub-processor; no training on hospital data |
| Belgian eHealth law | Therapeutic relationship and consent for the eHealth exchange |

To confirm with regulatory, legal and the DPO.

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
