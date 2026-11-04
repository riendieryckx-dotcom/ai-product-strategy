# My AI Product Strategy

> A living strategy built across 6 sessions. Each module adds one component. By Module 6, this repo IS your strategy — version-controlled, board-ready, portable.

---

## Strategy at a Glance

| Component | Module | Status | Key Artifact |
|-----------|--------|--------|-------------|
| **The Bet** | M1 | [x] | `01-the-bet/` |
| **The Moat** | M2 | [x] | `02-the-moat/` |
| **The Margin** | M3 | [x] | `03-the-margin/` |
| **The Contract** | M4 | [x] | `04-the-contract/` |
| **The Guardrails** | M5 | [ ] | `05-the-guardrails/` |
| **The Pitch** | M6 | [ ] | `06-the-pitch/` |

---

## The Bet (M1)

**What we're building, for whom, why now.**

- **Product:** Relevant History (working name) — a clinical decision support module in a hospital EHR for physicians on internal medicine wards. It shows the findings from the patient's own history that fit the current picture, and suggests possible diagnoses with a likelihood label and the estimated chance of major or extreme severity, updated with every new result. The physician decides.
- **AI Value Archetype:** Copilot
- **Vulnerability Scores:** Moat 4/5 · Data 3/5 · Platform 2/5
- **Top Risk:** Platform Exposure — differential reasoning is becoming a commodity, and our regulatory weight makes us slow to respond.
- **Confidence:** M — the data position and the place in the workflow are strong; the classification, the legal basis for outcome data and the clinical value are not yet proven.
- **Prototype:** [Relevant History – prototype](https://claude.ai/artifact/NYFskdj1szmhGDcKuRVgWQ) (synthetic patient)
- **Kill Criteria:** stop if the top 5 is no better than a list based on how common each diagnosis is, if the severity percentage does not separate severe stays better than admission data, if physicians open the module in fewer than half of eligible stays, or if there is no path to clinical use within 36 months or no legal basis for calibration.

→ Details: [`01-the-bet/`](01-the-bet/)

---

## The Moat (M2)

**Why this won't get copied in 6 months.**

- **Data Flywheel Score:** 12/20
- **Weakest Loop:** Preference (2/5) — calibrated per hospital, but the same for every physician on purpose.
- **Competitive Position:** Two axes: access to the patient's full record and its updates (low to high), and certified for diagnostic support in a European hospital (no to yes). We aim for high and yes. OpenAI ChatGPT for Healthcare sits at low record access (only what a hospital connects) and not certified for this use. Microsoft Dragon Copilot sits at medium record access (the conversation and the note) and not certified for this use. A specialised diagnostic vendor such as Isabel DDx sits at low record access, with its European certification status to verify. Draft placement, to check before presenting.
- **Encroachment Defense:** suggestions grounded in the full history and calibrated on each hospital's confirmed outcomes, the certified status, and a module that can be called from wherever the physician works, including from a documentation assistant.
- **Vendor Portability:** Partial — Google Gemini on Vertex AI is the primary model; "ready" means ready to switch to a validated open-weight standby, not to any new model.

→ Details: [`02-the-moat/`](02-the-moat/)

---

## The Margin (M3)

**Will this make money or bleed it?**

- **Gross Margin (current):** Not applicable — the EHR has no diagnostic support module today, so there is no current margin to compare with.
- **Gross Margin (AI-adjusted):** about 67%, rising to about 74% once clinical review falls to 3 hours; about 45% while the one-off certification is earned back. Illustrative assumptions.
- **Pricing Model:** hybrid — a fixed €5,000 per hospital per month, tiered by volume, with a 10% credit for a quarter in which the reliability contract's accuracy target is missed; not per suggestion, seat or clinical outcome.
- **Cascading Strategy:** Gemini Flash-class on every new result; Gemini Pro-class only when the selected findings change, a result is out of range, or the physician asks, and always for a possible severity of 40% or more (expected 80% triage only, 20% both).
- **Break-even at:** about 240 hospital-months of use (for example 20 hospitals for 12 months) to earn back the assumed €800,000 certification from the €3,367 contribution per hospital per month. Development costs are not included.

→ Details: [`03-the-margin/`](03-the-margin/)

---

## The Contract (M4)

**Why users will trust a probabilistic system.**

- **Reliability Target:** the confirmed diagnosis in the top 5 in at least 85% of stays, and at least 10 points above a list based on how common each diagnosis is; no claim shown to a physician that is not in the record.
- **Golden Dataset:** 12 rows, 4 adversarial
- **Confidence UX:** three tiers based on the chance that the confirmed diagnosis is in the list; below 50% no ranked list is shown, only the reason and the history findings; never auto-applied in any tier.
- **HITL Architecture:** the treating physician confirms each diagnosis and severity at discharge; triggered reviews stay at 100%; a random sample for post-market surveillance drops from 5% to 2%, never to zero.
- **Failure Mode Coverage:** covered in the golden rows: ungrounded claims, test, treatment or dose content, prompt injection, conflicting reports, negated findings, referral questions, known diagnoses, missing history and threshold cases. Not yet covered: rare diagnoses, severity 4 stays and records in French.

→ Details: [`04-the-contract/`](04-the-contract/)

---

## The Guardrails (M5)

**What breaks when this scales — and what compounds.**

- **Compounding System:** [describe feedback loops]
- **Governance Posture:** [approach]
- **Shadow AI Status:** __ tools found, __ triaged
- **Agent Boundaries:**
- **Regulatory Exposure:** likely a medical device in class IIb under the MDR, a high-risk AI system under the EU AI Act, and health data under GDPR article 9. The vendor is the manufacturer under the MDR and the processor under the GDPR; each hospital is the data controller. To confirm with regulatory, legal and the DPO.

→ Details: [`05-the-guardrails/`](05-the-guardrails/)

---

## The Pitch (M6)

**How you get this funded, shipped, and adopted.**

- **Horizon 1 (Now):**
- **Horizon 2 (Next):**
- **Horizon 3 (Bet):**
- **Board Narrative:** [1-sentence thesis]
- **Key Metric:**

→ Details: [`06-the-pitch/`](06-the-pitch/)

---

> Written from the perspective of the EHR vendor, which builds, certifies and sells the module; hospitals buy and use it. All data in this repo is synthetic. No real patient data, prices or customer data are used. Every file has a Dutch translation (`*.nl.md`); English is the source.
