# Cost Curve & Pricing Strategy

> **All figures are illustrative assumptions, not real prices or customer data.** Unit: one hospital, first scope (internal medicine), per month. Amounts in EUR. Every assumption is listed at the end.

## Cost Model

| Cost Category | Per-User/Month | Notes |
|--------------|----------------|-------|
| Inference (primary model) | €80 | Stronger model for the diagnosis suggestions and severity percentages, on the 40% of updates where the picture changes (720 calls), plus a share of the validation runs before each release. |
| Inference (cascading/triage) | €11 | Small model on every update (1,800 per month) to select the history findings that fit the current picture and to decide whether the suggestions need to be recalculated. |
| Infrastructure | €400 | Indexing the record for search, compute for the module and the gateway, in an EU region. |
| Data/storage | €150 | Search index of the record, and an audit log of every suggestion shown and every mark, kept for post-market surveillance. |
| Human-in-the-loop | €1,020 | Clinical review of a sample of suggestions (6 hours at €120) and a share of post-market surveillance and vigilance work (€300). |
| **Total AI COGS** | **€1,661** | Inference is about 5% of the total; clinical review is about 60%. |

## Cascading Strategy

**Triage model:** Gemini Flash-class on Vertex AI (EU region): a small, fast model that reads the current stay and the indexed history and selects the candidate findings. It runs on every new result.
**Frontier model:** Gemini Pro-class on Vertex AI (EU region): a stronger model that writes the diagnosis suggestions, likelihood labels and severity percentages from the selected findings.
**Routing rule:** The frontier model runs only when the selected findings change, when a new result is outside its reference range, or when the physician asks for an update. Otherwise the last suggestions stay, marked with the time they were made.
**Expected cascade ratio:** 60% triage only, 40% triage and frontier model.

Both models, and a validated open-weight standby that can also run on our on-premise OpenShift, are part of the certified product (see `02-the-moat/kill-switch.md`). Switching to another model is a change that needs validation, so the standby is validated in advance.

## Pricing Model

**Current pricing:** The EHR licence has no diagnostic support module; physicians search the history by hand.
**Proposed AI pricing:** An add-on licence of €5,000 per hospital per month for the first scope, in tiers by the number of eligible stays per month. Each new workup in scope is a paid extension of the same module.
**Model:** hybrid (fixed fee per hospital, tiered by volume). Not per suggestion: a price per suggestion would reward showing more suggestions, and hospitals budget for fixed costs.

## Stress Tests

| Scenario | Impact on Margin | Response |
|----------|-----------------|----------|
| Inference costs 3x | Inference rises from €91 to €273; gross margin from 67% to 63%. | Small impact, because inference is a small part of the cost. Raise the triage-only share and reuse suggestions until the picture changes. |
| Heaviest segment doubles | A large hospital with twice the stays: COGS rises to about €2,190; at the same price, margin falls to 56%. | Tiered price (€8,000 for the largest tier) brings margin back to about 73%. Clinical review scales by sample, not by stay. |
| Model provider raises prices 50% | Inference rises by about €45; margin falls to 66%. | Accept in the short term; switch to the validated standby model at the next planned release if the gap stays. |

The real margin risk is not inference but clinical review and certification. If the notified body asks for a larger review sample, clinical review is the line that grows.

## Board One-Pager

**Before (traditional SaaS):** EHR licence revenue only. No diagnostic support; the cost of searching the history sits with the physician, unmeasured.
**After (AI-enabled):** For 20 hospitals: €1.2M revenue per year, €0.4M AI COGS, gross margin 67%. Including the one-off certification and clinical evaluation (assumed €800,000, spread over 20 hospitals and 36 months, about €1,110 per hospital per month), the margin is about 45% in the first three years.
**Net margin shift:** Lower than a classic software add-on without clinical review, because the product carries certification and ongoing clinical review. After the certification cost is earned back, the margin moves back to about 67%, and each new workup in scope reuses the same certification file, quality system and infrastructure.

---

## Assumptions

- 300 eligible stays per hospital per month in the first scope, 6 updates per stay (admission plus new results): 1,800 updates.
- Models: Google Gemini on Vertex AI, EU region. The assumed prices below are above current list prices, to leave room for long context, thinking tokens and price changes.
- Triage model: about 15,000 input and 500 output tokens per update; assumed price €0.30 per million input tokens and €2.50 per million output tokens.
- Frontier model: about 20,000 input and 1,500 output tokens per call; assumed price €2.70 per million input tokens and €13.50 per million output tokens; €25 per month for validation runs.
- Clinical review: 6 hours per hospital per month at €120 per hour; post-market surveillance share €300 per hospital per month.
- One-off certification and clinical evaluation: €800,000 for a class IIb module, an order of magnitude to be replaced by a real estimate from regulatory.
- 20 hospitals on the module after 3 years.
- Price: €5,000 per hospital per month, €8,000 for the largest tier; a price hypothesis to test with customers, not a quote.
- Hosting in an EU region and the location of the models need review by security, legal and the DPO.
