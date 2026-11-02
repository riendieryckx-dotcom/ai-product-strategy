# Data Flywheel Map

> Score each loop 1-5. Your weakest loop is where competitors attack first.
> The four loops below are the M2 starting point - adapt if your product has 2 or 6 loops instead of 4.

## Flywheel Loops

| Loop | What It Measures | Score 1 | Score 5 | Score |
|------|------------------|---------|---------|-------|
| **Correction** | Do users fix AI outputs? Is that signal captured and reused? | No capture | Automated retraining | 4/5 |
| **Preference** | Does the product learn individual / team preferences over time? | Stateless | Deep personalization | 2/5 |
| **Domain Context** | Does usage in one area improve quality in adjacent areas? | Siloed | Cross-domain transfer | 3/5 |
| **Network** | Does each new user / team make the product better for everyone? | Isolated | Strong network effects | 3/5 |

### Correction Loop - 4/5
**What you capture today:** Three signals per stay: the physician's "relevant / not relevant" mark on each history finding, the "consider / not applicable" mark on each suggested diagnosis, and, at discharge, the confirmed diagnoses and severity of illness coded for the mandatory hospital registration. The last one needs no extra work from the physician.

**How it compounds:** At discharge, the treating physician confirms the diagnosis and severity with one click in the discharge workflow; only confirmed stays are used. The model then recalibrates its likelihood labels and severity percentages automatically every week, on confirmed labels only, within limits set in advance in the technical documentation (for example a maximum shift of the severity percentages per update). Before each recalibration goes live, the golden suite from Module 4 runs automatically; if it fails, the update is not activated. The physicians' marks improve which findings are shown. Changes outside those limits, and changes to the model itself, go through planned, validated releases. Not a 5, because the model itself is not retrained automatically, and how far these limits may go still needs confirmation from regulatory and the notified body. Suggestions that physicians follow can also shape the outcome they are measured against, so part of each check is done on stays where the module was not shown.

### Preference Loop - 2/5
**What you capture today:** Every confirmed discharge diagnosis and severity of illness, per hospital. The suggestions and severity percentages are the same for every physician on purpose, but they are calibrated on each hospital's own patients.

**How it compounds:** With each confirmed diagnosis, the model becomes more accurate for this hospital's patients: likelihood labels and severity percentages are recalibrated on its own outcomes. That learning reaches physicians through the weekly recalibration described in the Correction loop: on physician-confirmed labels, within limits set in advance, and only after the golden suite passes. Not higher than 2, because nothing adapts per physician or ward: clinical logic that changes per physician would be hard to validate and would weaken the evidence for certification.

### Domain Context Loop - 3/5
**What you capture today:** The link between history findings and the current picture (for example earlier low ferritin and a current anaemia), per first-scope workup (anaemia, fever, weight loss).

**How it compounds:** Many history findings matter across workups (kidney function, earlier endoscopies, medication), so each new workup starts with links already validated in the previous one. Each new workup still needs its own clinical evaluation before use.

### Network Loop - 3/5
**What you capture today:** Confirmed outcomes per hospital, on the same EHR and the same coding rules.

**How it compounds:** Each hospital that joins adds confirmed outcomes for calibration, which matters most for rare diagnoses and for severity 4, where one hospital has too few stays. Capped at 3 because this pooling needs a legal basis and agreements per hospital; without it, every hospital calibrates on its own data only.

**Total Flywheel Score: 12/20**
**Weakest Loop:** Preference
**Fix for weakest loop:** Keep the clinical logic the same for everyone, but let each ward set what it sees: which workups are switched on, how many suggestions are shown, and from which severity percentage a suggestion is highlighted. That adds stickiness without changing the certified logic. The bigger fix goes to Correction, because that is where an attacker would aim: publish per-hospital measurements (how often the confirmed diagnosis was in the top 5, and how well the severity percentages matched) so hospitals see that the module gets better with their own data.

---

## Encroachment Threat Assessment

### 1. Platform Encroachment
**Attacker:** OpenAI ChatGPT for Healthcare
**Vector:** A hospital connects it to the EHR through FHIR, and physicians ask it for a differential diagnosis with likelihoods and sources.
**Time-to-threat:** Unofficial use by individual physicians is already possible; official use for diagnosis in a European hospital needs certification and European availability, an estimated 2–3 years.
**% of value at risk:** 40% (estimate)

### 2. Vertical Competitor
**Attacker:** A specialised diagnostic decision support vendor (for example Isabel DDx)
**Vector:** An integration into the EHR through FHIR, with years of experience in diagnostic reasoning and an existing clinical customer base.
**Time-to-threat:** 1–2 years, depending on its European certification and an integration with our EHR.
**% of value at risk:** 20% (estimate)

### 3. Adjacent Expansion
**Attacker:** Microsoft Dragon Copilot
**Vector:** From ambient documentation, where it already listens to the consultation and writes the note, into decision support inside the same workflow.
**Time-to-threat:** 1–2 years
**% of value at risk:** 30% (estimate)

---

## 90-Day Encroachment Plan

*Your partner played the Big Tech attacker. What was their plan to kill you?*

**Attacker:** Microsoft Dragon Copilot
**Attack vector (target the weakest loop):** Preference: offer each physician a personal assistant that learns how they work, against a module that behaves the same for everyone.
**Weeks 1-4 - what they ship:** A free pilot for one hospital that already uses ambient documentation, with a differential diagnosis drawn from the conversation and the note.
**Weeks 5-8 - how they poach users:** Physicians who already like the documentation get the differential in the same window, with no extra screen, and it adapts to their style.
**Weeks 9-12 - why users don't come back:** The assistant feels personal and is where they already write; our module feels like a second screen.
**Your defense:** Our suggestions are grounded in the full history, not only in today's conversation, and calibrated on confirmed outcomes in this hospital. We show that with per-hospital measurements, and we make the module open from wherever the physician works, including from a documentation assistant through an integration.

> All percentages and time-to-threat values are estimates for discussion, not measurements. The 90-day plan is a draft; replace it with the plan your partner played in class.
