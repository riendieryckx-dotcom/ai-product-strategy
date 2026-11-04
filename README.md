# My AI Product Strategy

> A living strategy built across 6 sessions. Each module adds one component. By Module 6, this repo IS your strategy — version-controlled, board-ready, portable.

---

## Strategy at a Glance

| Component | Module | Status | Key Artifact |
|-----------|--------|--------|-------------|
| **The Bet** | M1 | [OK] | `01-the-bet/` |
| **The Moat** | M2 | [OK] | `02-the-moat/` |
| **The Margin** | M3 | [OK] | `03-the-margin/` |
| **The Contract** | M4 | [OK] | `04-the-contract/` |
| **The Guardrails** | M5 | [OK] | `05-the-guardrails/` |
| **The Pitch** | M6 | [ ] | `06-the-pitch/` |

---

## The Bet (M1)

**What we're building, for whom, why now.**

- **Product:** Relevant History — clinical decision support in a hospital EHR, during a stay or an outpatient workup: findings from the patient's own history and diagnosis suggestions with an estimated severity, updated with every new result. The physician decides.
- **AI Value Archetype:** Copilot
- **Vulnerability Scores:** Moat 4/5 · Data 3/5 · Platform 2/5
- **Top Risk:** Platform Exposure — differential reasoning is becoming a commodity, and we pivot slowly.
- **Confidence:** M — strong data and workflow position; classification, legal basis and clinical value still to prove.
- **Prototype:** [Relevant History – prototype](https://claude.ai/artifact/NYFskdj1szmhGDcKuRVgWQ) (synthetic patient)
- **Kill Criteria:** stop if the list beats no simple baseline, physicians do not diagnose better, tests rise without benefit, the module goes unused, or certification or the legal basis fails.

→ Details: [`01-the-bet/`](01-the-bet/)

---

## The Moat (M2)

**Why this won't get copied in 6 months.**

- **Data Flywheel Score:** 12/20
- **Weakest Loop:** Preference (2/5) — calibrated per hospital, the same for every physician on purpose.
- **Competitive Position:** axes: access to the full record (low–high) and certified for diagnostic support in the EU (no–yes). We aim for high and yes; ChatGPT for Healthcare is low and no, Dragon Copilot medium and no, Isabel DDx low with its EU status to verify. Draft placement.
- **Encroachment Defense:** grounded in the full history, calibrated on each hospital's outcomes, certified, and callable from other tools.
- **Vendor Portability:** Partial — Google Gemini primary; ready only for a validated open-weight standby.

→ Details: [`02-the-moat/`](02-the-moat/)

---

## The Margin (M3)

**Will this make money or bleed it?**

- **Gross Margin (current):** not applicable — no diagnostic support module today.
- **Gross Margin (AI-adjusted):** about 71%, about 78% later, about 55% while certification is earned back. Illustrative.
- **Pricing Model:** hybrid — €7,000 per hospital per month (€5,000 stays, €2,000 outpatient), tiered, with a 10% reliability credit.
- **Cascading Strategy:** Gemini Flash-class on every result, Pro-class when the picture changes or severity can be high (80/20).
- **Break-even at:** about 160 hospital-months to earn back the assumed €800,000 certification (€4,953 contribution per month); development not included.

→ Details: [`03-the-margin/`](03-the-margin/)

---

## The Contract (M4)

**Why users will trust a probabilistic system.**

- **Reliability Target:** top 5 ≥85% and 10 points above baseline; must-not-miss ≥95%; confidence tiers that hold; no ungrounded claim shown.
- **Golden Dataset:** 105 rows, 10 adversarial; 47 standard (45%), 15 outpatient; labelled by two physicians, from unpublished records
- **Confidence UX:** high >90%, medium 70–90%, low <70% with no ranked list and a review; never auto-applied.
- **HITL Architecture:** the treating physician confirms labels at discharge; the vendor's clinical team reviews triggers and a 5% → 2% sample.
- **Failure Mode Coverage:** adversarial, must-not-miss, subgroups, data quality, stability, grounding and outpatient follow-up covered; rare diagnoses and the effect on physicians not yet.

→ Details: [`04-the-contract/`](04-the-contract/)

---

## The Guardrails (M5)

**What breaks when this scales — and what compounds.**

- **Compounding System:** three loops (recursive learning, cross-domain transfer, network intelligence): one broken, two missing. Freeze test: still winning today, so we scale until the recalibration loop ships.
- **Governance Posture:** the module never writes to the record; six escalation triggers; audit from real time to quarterly with named roles; Level 2 today, Level 3 target.
- **Shadow AI Status:** 5 workarounds (hypotheses), 5 triaged: 2 build, 2 partner, 1 ignore
- **Agent Boundaries:** two read-only models without memory behind a gateway that stops the chain on a failed check.
- **Regulatory Exposure:** likely MDR class IIb, EU AI Act high risk, GDPR article 9. The vendor is manufacturer and processor; each hospital is data controller. To confirm with regulatory, legal and the DPO.

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

> Written from the perspective of the EHR vendor. All data is synthetic. Every file has a Dutch translation (`*.nl.md`); English is the source.
