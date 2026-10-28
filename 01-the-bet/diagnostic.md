# Three-Axis Vulnerability Diagnostic

## Product

**Product:** Comparable Patients (working name) — a module in our hospital EHR that shows, for a given patient profile, how comparable patients were treated (care path variants A, B, C and their share) and what happened next (length of stay, 30-day readmissions), both in the user's own hospital and across all hospitals on the same EHR, pooled and pseudonymised. It describes practice and outcomes; it does not recommend a treatment. First users are care path committees and quality teams; physicians at the bedside come later.

**Your Role:** Product & Strategy lead at the market-leading hospital EHR vendor in Flanders; owner of this bet.

---

## Scores

### Contextual Moat — 4/5
*Workflow depth × switching cost. Would users leave in a weekend if a competitor showed up?*

**Score rationale:** The data is created in our EHR across many hospitals; a single hospital's data team can analyse its own data, but only the network operator can show how its practice compares with other hospitals.

**Named attacker (from partner challenge):** Microsoft Fabric healthcare data solutions — turns EHR data into the OMOP model and lets a hospital's data team build patient cohorts on its own data. https://learn.microsoft.com/en-gb/industry/healthcare/healthcare-data-solutions/overview

---

### Data Advantage — 4/5
*Proprietary signal that compounds with usage. What do you see that OpenAI doesn't?*

**Score rationale:** Every hospital that joins enlarges the cohorts for all others, every discharge adds a new outcome automatically, and readmissions in another hospital on the same system become visible; not a 5, because pooling depends on a legal basis and an agreement with every hospital.

**Named attacker (from partner challenge):** Epic Cosmos / CoMET — the same pooled-network model at a far larger scale (300M+ patients, 310 health systems), already forecasting length of stay and readmission. https://www.microsoft.com/en-us/research/?p=1148919

---

### Platform Exposure — 4/5
*Encroachment risk × pivot speed. If Apple/Google/OpenAI ships your hero feature native — then what?*

**Score rationale:** A consumer health model can explain guidelines, but it cannot see how patients in Belgian hospitals were treated or what happened to them; pivot speed is reasonable because the product describes rather than recommends.

**Named attacker (from partner challenge):** Meta Muse Spark — free, health-focused model trained with 1,000+ physicians. https://about.fb.com/news/2026/04/introducing-muse-spark-meta-superintelligence-labs/

---

## Top Vulnerability
The moat only exists if hospitals agree to pool their data: without a legal basis for secondary use and trust that no hospital is exposed to its competitors, the network shrinks to single-hospital data that any data team can analyse. Second risk: users read "comparable patients did better with C" as a recommendation, while the difference may reflect which patients (or which hospitals' populations) got C.

## Confidence Level
M — the data and network position is strong and the use case is new, but data pooling, comparability and confounding are unproven.
