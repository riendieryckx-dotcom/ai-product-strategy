# Three-Axis Vulnerability Diagnostic

## Product

**Product:** Relevant History (working name) — a clinical decision support module in our hospital EHR for physicians on internal medicine wards. It combines historical data (the patient's earlier stays, problem list, lab trends, medication, reports and letters, including those from other hospitals shared through the existing eHealth exchange) with new data from the current stay. It shows two things: the findings from the history that fit the current picture and are not yet in the current notes, and a short list of possible diagnoses. Each diagnosis has a likelihood label, the estimated chance that the stay reaches major or extreme severity (APR-DRG severity of illness 3–4) if it is confirmed, and links to the findings that support it. Every new result updates both lists and shows what changed. The physician decides; the module never replaces clinical judgement. First scope: adults on internal medicine wards with a diagnostic workup that is not yet clear (for example unexplained anaemia, fever or weight loss).

**Your Role:** Product & Strategy lead at the market-leading hospital EHR vendor in Flanders; owner of this bet.

---

## Scores

### Contextual Moat — 4/5
*Workflow depth × switching cost. Would users leave in a weekend if a competitor showed up?*

**Score rationale:** The module sits in the clinical workstation where the history and every new result already land, and as a CE-marked medical device it is the version a hospital can officially use for diagnostic support; replacing a hospital EHR takes years. Not a 5, because a third-party assistant can plug into the same workflow through integrations, and the certification lead is temporary (estimated 2–3 years), not permanent.

**Named attacker (from partner challenge):** Microsoft Dragon Copilot — clinical assistant with built-in, evidence-based decision support inside the EHR workflow. https://www.microsoft.com/en-us/health-solutions/clinical-workflow/dragon-copilot

---

### Data Advantage — 3/5
*Proprietary signal that compounds with usage. What do you see that OpenAI doesn't?*

**Score rationale:** Every discharge gives us the confirmed diagnoses and the severity of illness of the stay, coded for the mandatory hospital registration, so we can measure each suggestion and calibrate its severity percentage on real outcomes. Physicians' marks on findings and suggestions add a correction signal. Capped at 3 because hospitals are the data controllers and we are their processor, so calibrating our product on their outcomes needs a legal basis and an agreement per hospital, and more so across hospitals; coded diagnoses follow registration rules rather than clinical truth, and suggestions that physicians follow can influence the labels they are measured against.

**Named attacker (from partner challenge):** Epic Cosmos / CoMET — diagnosis prediction trained on records of 300M+ patients from 310 health systems. https://www.microsoft.com/en-us/research/?p=1148919

---

### Platform Exposure — 2/5
*Encroachment risk × pivot speed. If Apple/Google/OpenAI ships your hero feature native — then what?*

**Score rationale:** General health models already produce a prioritised differential with likelihoods and cited sources, but the reasoning alone is not the product: diagnostic support always needs medical validation, with a clinical evaluation for the intended purpose and certification, before a hospital can use it officially. A platform that ships the feature natively has to go through the same validation, and that validation belongs to the product, not to the model. What general models also lack is the record, its updates and calibration on confirmed outcomes. Pivot speed is low: a module that suggests diagnoses with a severity estimate is likely class IIb, so every change to the model or intended purpose needs new evidence and assessment.

**Named attacker (from partner challenge):** OpenAI ChatGPT for Healthcare — enterprise product for hospitals with a clinical reasoning view that shows a differential diagnosis table with likelihoods and sources. https://openai.com/index/openai-for-healthcare/

---

## Top Vulnerability

**Platform Exposure.** Differential reasoning is becoming a commodity, and our regulatory weight makes us slow to respond. The defence is not a better list, but a list that is always current with the patient's record, grounded in its findings, and calibrated on confirmed outcomes, built up during the 2–3 years before general models are certified for this use.
