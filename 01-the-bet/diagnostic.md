# Three-Axis Vulnerability Diagnostic

## Product

**Product:** Relevant History (working name) — a clinical decision support module in our hospital EHR. For physicians in internal medicine, during a hospital stay or an outpatient workup, it shows the findings from the patient's own history that fit the current picture and are not yet in the notes, and up to five possible diagnoses. Each has a likelihood label and the chance of a serious course if confirmed: in a stay, APR-DRG severity 3–4; in outpatient care, an unplanned admission within 30 days. Every new result updates both lists. The physician decides. First scope: unclear workups such as anaemia, fever or weight loss, on the ward and in the outpatient clinic.

**Your Role:** Product & Strategy lead at the market-leading hospital EHR vendor in Flanders; owner of this bet.

---

## Scores

### Contextual Moat — 4/5
*Workflow depth × switching cost. Would users leave in a weekend if a competitor showed up?*

**Score rationale:** The module sits where the history and every new result already land, on the ward and in the outpatient clinic, and as a CE-marked device it is the version a hospital may officially use. Not a 5: others can integrate, and the certification lead (2–3 years) is temporary.

**Named attacker (from partner challenge):** Microsoft Dragon Copilot — clinical assistant with decision support inside the EHR workflow. https://www.microsoft.com/en-us/health-solutions/clinical-workflow/dragon-copilot

---

### Data Advantage — 3/5
*Proprietary signal that compounds with usage. What do you see that OpenAI doesn't?*

**Score rationale:** Every discharge confirms the diagnoses and severity, and every closed outpatient workup confirms a diagnosis, so each suggestion can be measured and calibrated on real outcomes. Capped at 3: hospitals are the data controllers and we are their processor, coded diagnoses are not always clinical truth, outpatient diagnoses are not coded for the hospital registration and arrive later, and followed suggestions can shape their own labels.

**Named attacker (from partner challenge):** Epic Cosmos / CoMET — diagnosis prediction trained on records of 300M+ patients. https://www.microsoft.com/en-us/research/?p=1148919

---

### Platform Exposure — 2/5
*Encroachment risk × pivot speed. If Apple/Google/OpenAI ships your hero feature native — then what?*

**Score rationale:** General models already write differentials, but diagnostic support always needs medical validation and certification for its intended purpose, and that belongs to the product, not to the model. Our own pivots are slow: the module is likely class IIb.

**Named attacker (from partner challenge):** OpenAI ChatGPT for Healthcare — shows a differential with likelihoods and sources. https://openai.com/index/openai-for-healthcare/

---

## Top Vulnerability

**Platform Exposure.** Differential reasoning is becoming a commodity. Our defence is a list that is current with the record, grounded in it and calibrated on confirmed outcomes, built in the 2–3 years before general models are certified for this use.
