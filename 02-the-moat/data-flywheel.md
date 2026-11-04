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
**What you capture today:** the physician's marks on findings ("relevant / not relevant") and suggestions ("consider / not applicable"), and at discharge or when an outpatient workup is closed, the diagnosis (in a stay also the severity), confirmed by the treating physician with one click.

**How it compounds:** likelihood and severity are recalibrated every week on confirmed labels only, within limits set in the technical documentation, and only after the golden suite passes; bigger changes go through validated releases. Not a 5: the model itself is not retrained automatically, and regulatory must confirm the limits. Results are compared with a baseline before go-live, because followed suggestions shape their own labels.

### Preference Loop - 2/5
**What you capture today:** confirmed outcomes per hospital; the logic is the same for every physician on purpose.

**How it compounds:** each confirmed diagnosis makes the module more accurate for that hospital's patients. Not higher: logic that changes per physician is hard to validate.

### Domain Context Loop - 3/5
**What you capture today:** links between history findings and the current picture, per workup (anaemia, fever, weight loss).

**How it compounds:** findings such as kidney function, endoscopies or medication matter across workups and across settings: links learned in stays carry over to outpatient workups and back. Each new workup or setting still needs its own clinical evaluation.

### Network Loop - 3/5
**What you capture today:** confirmed outcomes per hospital, from stays and outpatient workups, on one EHR and one coding standard.

**How it compounds:** each hospital adds outcomes for calibration, which matters most for rare diagnoses and severity 4. Capped at 3: as processor, pooling for our own product needs a legal basis and an agreement per hospital.

**Total Flywheel Score: 12/20**
**Weakest Loop:** Preference
**Fix for weakest loop:** ward-level settings (which workups, how many suggestions, from which severity a suggestion is highlighted) that leave the certified logic unchanged, plus per-hospital reports that show the module improving on the hospital's own data.

---

## Encroachment Threat Assessment

### 1. Platform Encroachment
**Attacker:** OpenAI ChatGPT for Healthcare
**Vector:** connected to the EHR through FHIR and asked for a differential with likelihoods.
**Time-to-threat:** unofficial use is already possible; official use in an EU hospital needs certification, an estimated 2–3 years.
**% of value at risk:** 40% (estimate)

### 2. Vertical Competitor
**Attacker:** a specialised diagnostic decision support vendor (for example Isabel DDx)
**Vector:** a FHIR integration into the EHR, with an existing clinical customer base.
**Time-to-threat:** 1–2 years, depending on EU certification and integration.
**% of value at risk:** 20% (estimate)

### 3. Adjacent Expansion
**Attacker:** Microsoft Dragon Copilot
**Vector:** from ambient documentation into decision support in the same workflow.
**Time-to-threat:** 1–2 years
**% of value at risk:** 30% (estimate)

---

## 90-Day Encroachment Plan

*Your partner played the Big Tech attacker. What was their plan to kill you?*

**Attacker:** Microsoft Dragon Copilot
**Attack vector (target the weakest loop):** Preference: a personal assistant that learns how each physician works.
**Weeks 1-4 - what they ship:** a free pilot with a differential drawn from the conversation and the note, in a hospital that already uses ambient documentation.
**Weeks 5-8 - how they poach users:** the differential appears in the window physicians already use, adapted to their style.
**Weeks 9-12 - why users don't come back:** it feels personal and needs no second screen.
**Your defense:** suggestions grounded in the full history and calibrated on this hospital's outcomes, shown in per-hospital reports, and callable from wherever the physician works, including a documentation assistant.

> All percentages and times are estimates. Replace the 90-day plan with the one your partner played in class.
