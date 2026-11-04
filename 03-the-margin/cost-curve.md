# Cost Curve & Pricing Strategy

> **Illustrative assumptions, not real prices or customer data.** Unit: one hospital, first scope (stays and outpatient consultations), per month, in EUR.

## Cost Model

| Cost Category | Per-User/Month | Notes |
|--------------|----------------|-------|
| Inference (primary model) | €70 | Gemini Pro-class on 20% of updates (600 calls), plus validation runs. |
| Inference (cascading/triage) | €17 | Gemini Flash-class on every update (3,000: 1,800 from stays, 1,200 from consultations). |
| Infrastructure | €500 | Record index, compute and gateway in an EU region, for both settings. |
| Data/storage | €200 | Index, plus an audit log of every suggestion and mark for post-market surveillance. |
| Human-in-the-loop | €1,260 | The vendor's clinical review (8 hours at €120) and surveillance (€300); €780 once the review sample drops to 2%. |
| **Total AI COGS** | **€2,047** | €1,567 later. Inference is about 4%, clinical review about 60%. |

**Cost for the hospital (not in AI COGS):** about 100 minutes of physician time per month to confirm diagnoses at discharge and when outpatient workups are closed.

## Cascading Strategy

**Triage model:** Gemini Flash-class (Vertex AI, EU region): selects the history findings on every new result.
**Frontier model:** Gemini Pro-class: writes the suggestions, likelihood labels and severity percentages.
**Routing rule:** the frontier model runs only when the selected findings change, a result is out of range, a severity of 40% or more is possible, or the physician asks and the findings changed. Otherwise the last list stays, with its time. For a consultation, the list is prepared before the visit and updated when results arrive between visits, without interrupting the physician.
**Expected cascade ratio:** 80% triage only, 20% both. Both models and a validated open-weight standby are part of the certified product.

## Pricing Model

**Current pricing:** the EHR licence has no diagnostic support.
**Proposed AI pricing:** €7,000 per hospital per month (€5,000 for stays, €2,000 for outpatient consultations), tiered by volume; each new workup is a paid extension. A 10% credit for a quarter in which the Module 4 accuracy target is missed.
**Model:** hybrid. Not per suggestion (it would reward showing more), not per seat (value arises per stay), not per clinical outcome (an incentive that cannot be defended).

## Stress Tests

| Scenario | Impact on Margin | Response |
|----------|-----------------|----------|
| Inference costs 3x | €87 → €261; margin 71% → 68%. | Reuse lists until the picture changes; keep the 40% severity rule. |
| Heaviest segment doubles | COGS about €2,710; margin 61% at the same price. | The €11,000 tier brings it to about 75%; review scales by sample, not by stay. |
| Model provider raises prices 50% | +€44; margin stays about 70%. | Accept; move to the validated standby at the next release if needed. |

The margin risk is clinical review and certification, not inference: moving the cascade from 60/40 to 80/20 saves about €45 (0.6 point); halving review saves €480 (about 7 points).

## Board One-Pager

**Before (traditional SaaS):** EHR licence only; physicians search the history by hand.
**After (AI-enabled):** for 20 hospitals, €1.68M revenue and €0.49M AI COGS a year. Gross margin 71%, about 78% once review falls to 4 hours, and about 55% while the €800,000 certification is earned back over 36 months.
**Net margin shift:** lower than a classic add-on, because of certification and clinical review; each new workup reuses the same certification file, quality system and infrastructure.

## Hospital ROI

What one hospital pays and gets back per year. Both benefits must be proven in the pilot, against the baseline before go-live.

| Per hospital per year | Conservative | Base |
|---|---|---|
| Licence (€7,000 per month) | €84,000 | €84,000 |
| Physician time to confirm labels (about 100 minutes per month) | €2,400 | €2,400 |
| Implementation and training (year 1 only) | €20,000 | €20,000 |
| Physician time saved searching the history (900 stays and consultations per month) | 2 minutes each: €43,200 | 3 minutes each: €64,800 |
| Shorter stays from a faster diagnosis (3,600 stays per year) | none: €0 | 0.1 day each: €144,000 |
| **ROI, year 1** | **−59%** | **+96%** |
| **ROI, from year 2** | **−50%** | **+142%** |

The case rests on shorter stays, not on saved time. On time alone, the module needs about 4 minutes saved per encounter to break even. With 3 minutes saved, stays only need to shorten by about 0.015 day (about 20 minutes) on average. Saved time and freed bed-days are capacity, not cash, unless the hospital uses them for more patients.

Not counted, on purpose: avoided missed diagnoses (not measurable yet), effects on coding and financing (counting them would reward upcoding), and the risk of extra tests (a kill criterion in Module 1).

## Assumptions

- Per hospital per month: 300 eligible stays (1,800 updates) and 600 eligible outpatient consultations (1,200 updates: before the visit and when results arrive).
- Triage: about 15,000 input and 500 output tokens per update at €0.30 and €2.50 per million; frontier: about 20,000 and 1,500 at €2.70 and €13.50 per million, plus €25 for validation runs. Prices are set above Gemini list prices as a buffer.
- Review: 8 hours at €120 (4 hours once the sample is 2%), including the quarterly independent reference; surveillance €300.
- One-off: certification and clinical evaluation €800,000 (class IIb, to replace with a real estimate; an intended purpose that includes outpatient care may cost more); labelling the golden set about €3,000.
- 20 hospitals after 3 years; €7,000 per month (€11,000 for the top tier) is a hypothesis to test.
- Hospital ROI: physician time at €120 per hour; a freed bed-day valued at €400; implementation €20,000 in year 1.
- Roles: the vendor is manufacturer under the MDR and processor under the GDPR; each hospital is data controller. Hosting and model location to review with security, legal and the DPO.
