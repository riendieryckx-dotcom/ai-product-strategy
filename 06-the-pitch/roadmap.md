# Three-Horizon Roadmap & Board Pitch

## Roadmap

### Horizon 1 — Now (0-3 months)
*Quick wins. Ship with existing capabilities.*

| Initiative | Metric | Confidence |
|-----------|--------|-----------|
| Gateway and automated golden suite: model calls behind `dxGateway`, Gemini versions pinned, the 105 golden rows run on every change (Contract) | All 22 safety rows pass in the pipeline; every quality drop caught before release | H |
| Label audit: 200 retrospective stays, coded discharge diagnosis against a review by two physicians (Moat) | Agreement ≥80%; stop the calibration plans if below 80% | H |
| Vignette study: 12 internists, 40 cases from unpublished records, with and without the findings panel (Bet) | Key history finding found within 5 minutes ≥20 points more often, without more tests requested; stop the project if not met | M |
| Classification opinion and a first dialogue with a notified body, for the full case and for findings only (Guardrails) | Written opinion on the class and the path to clinical use; stop if no path within 36 months | M |
| Legal basis with 2 pilot hospitals: processor role, Google as sub-processor, use of outcomes, reading notes after display (Guardrails) | Signed agreement or a written no; without it, no pooling and no implicit-use loop | M |

### Horizon 2 — Next (3-9 months)
*Bets. Requires new capabilities or integrations.*

| Initiative | Metric | Confidence |
|-----------|--------|-----------|
| Retrospective test on pseudonymised data from 2 hospitals, stays and outpatient workups (Bet) | Top 5 ≥10 points above a list based on how common each diagnosis is; must-not-miss ≥95%; stop at month 6 if the top 5 does not beat that list | M |
| Silent mode in 2 hospitals: lists computed but not shown, implicit-use signals logged (Moat) | Precision of shown findings ≥2 in 3; signal in ≥70% of stays; stop the implicit-use loop if precision stays below 2 in 3 | M |
| Validated open-weight standby that also runs on-premise (Margin) | Passes all safety rows; at least 4 of the top 5 equal to Gemini; if not, no second route and the Provider risk stays H | M |
| Quality system for medical devices and the technical file: clinical evaluation plan, post-market surveillance plan (Guardrails) | Application to a notified body by month 9; stop if the certification estimate exceeds the Module 3 budget | L |

### Horizon 3 — Bet (9-18 months)
*Moonshots. High uncertainty, high potential.*

| Initiative | Metric | Confidence |
|-----------|--------|-----------|
| Supervised pilot: physicians see the module on 2 internal medicine wards and their outpatient clinics, within the clinical evaluation (Bet) | Physicians reach the confirmed diagnosis more often or sooner than in the baseline; tests per stay rise ≤10% | L |
| Pooled calibration and implicit use across all hospitals on the EHR, once each gave a legal basis (Moat) | Severity calibration within 5 points, also for severity 4; selection improves in every hospital that joins | L |
| Relevant History callable from other tools, including documentation assistants, through a standard decision-support integration (Moat) | One partner integration live; the competitor in the 90-day plan becomes a channel | L |

## Board Pitch

**Thesis (1 sentence):** Internists lose time and miss facts because a patient's history is scattered across years of stays, letters and other hospitals; we bring the findings that matter into their workflow with the source, suggest possible diagnoses with a measured severity, and get better on every confirmed outcome.

**The case:**
1. Why now: language models can now read Dutch and French clinical text in real time for about €87 per hospital per month, the eHealth exchange makes letters from other hospitals available, and general models may not be used for diagnosis in a European hospital until they are certified: a lead of an estimated 2–3 years.
2. What's defensible: the module sits where the record and every new result land; it learns from what physicians take over and from confirmed diagnoses on our installed base; the certified status and a 105-row golden set built from real failures stay with us; a validated standby model limits our dependence on Google.
3. The economics: about €2,047 AI cost per hospital per month, of which inference is about 4% and clinical review about 60%; €7,000 per hospital per month gives a 71% gross margin (55% while certification is earned back) and an inference ROI of about 80x. For the hospital, the case rests on shorter stays: +142% from year 2 in the base case, −50% if stays do not shorten.

**The risks:**
1. Trust / failure modes: the evidence says a good list alone does not make physicians better and can add tests, and followed suggestions can shape their own labels. Mitigation: confidence tiers, a gateway that blocks claims outside the record and any treatment or dose, 22 safety rows at 100%, and kill criteria on physician outcomes and tests.
2. Scale / governance: likely MDR class IIb (notified body reviews take 13–18 months), high risk under the AI Act, and health data where the hospital is controller and we are processor. The module never writes to the record; audits run from real time to quarterly with named owners.
3. Competitive: Google, OpenAI and Microsoft Dragon Copilot can offer differentials; the certification lead is temporary. Our answer is speed to working learning loops and being callable from their tools rather than fighting them.

**The ask:** a 9-month evidence phase (H1 and H2), not certification yet. One feature team that owns the clinical workstation flow end to end, on the existing product backlog with one product owner: 4 engineers (1 with clinical language processing experience), a 0.5 FTE internist as clinical lead, 0.3 FTE regulatory and 0.2 FTE legal and DPO, at internal rates [€__]. Non-people budget of about €35,000: physician hours for the label audit and the vignette study (about €15,000 at €120 per hour), cloud and models for the retrospective test and silent mode (about €10,000), and the first notified body dialogue (about €10,000, to confirm). Hard reviews at month 3 (vignette study, label audit) and month 9 (retrospective test, silent mode) against the kill criteria above. The certification decision (assumed €800,000) comes at month 9, on evidence.

## M1 Baseline vs. Now
*Your 3-sentence AI strategy from Module 1 vs. what you'd say now:*

**M1 baseline:** (reconstructed) We want to add an AI assistant to the clinical workstation that summarises the patient record. Physicians are overloaded, so anything that saves them time will be welcome. We'll start with a pilot in one hospital and see how it goes.

**Now:** We bet that internists will diagnose faster and miss less when our EHR brings forward what the patient's own history already shows and suggests possible diagnoses with a measured severity, because only we hold the full record, every new result and every confirmed outcome. Our moat is the place in the workflow, loops that learn from what physicians take over and from confirmed diagnoses, and a certified status general models lack; at €7,000 per hospital per month the margin is 71%, inference is 4% of the cost and clinical review is the real expense. We prove it first with a vignette study, a label audit and silent mode, under a reliability contract with 22 safety rows, a rule that the module never writes to the record, and kill criteria on physician outcomes — all live in the repo.
