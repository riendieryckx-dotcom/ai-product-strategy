# Data Flywheel Map

Product: Comparable Patients — how comparable patients were treated and what happened next, in the user's own hospital and across all hospitals on the same EHR.

## Flywheel Loops

| Loop | What It Measures | Score 1 | Score 5 | Score |
|------|------------------|---------|---------|-------|
| **Correction** | Do users fix AI outputs? Is that signal captured and reused? | No capture | Automated retraining | 2/5 |
| **Preference** | Does the product learn individual / team preferences over time? | Stateless | Deep personalization | 1/5 |
| **Domain Context** | Does usage in one area improve quality in adjacent areas? | Siloed | Cross-domain transfer | 3/5 |
| **Network** | Does each new user / team make the product better for everyone? | Isolated | Strong network effects | 4/5 |

### Correction Loop - 2/5
**What you capture today:** Outcomes update themselves: every discharge adds length of stay and every readmission is recorded, so the figures correct over time. No signal yet on whether users agree that the "comparable" patients really are comparable.

**How it compounds:** Clinical reviewers flag stays as "not comparable", with a reason. Across hospitals, those flags train the similarity rules, so comparability becomes clinically validated rather than a technical guess — the part a hospital data team cannot copy. Next step: when a committee changes a care path, it records the change and the date, and later outcomes are shown before and after the change, next to the network trend. Each hospital's improvements then become evidence for the others.

### Preference Loop - 1/5
**What you capture today:** Nothing. Every committee sees the same view.

**How it compounds:** Saved profiles and views per care path committee. Deliberately low priority: personal preferences add little to a shared, factual view and could make hospitals see different versions of the truth.

### Domain Context Loop - 3/5
**What you capture today:** One data model for all conditions: diagnoses, severity, procedures, length of stay and readmissions are coded the same way across care paths and hospitals.

**How it compounds:** Comparability rules and selection checks built for hip fracture (age, frailty, anticoagulants, severity) transfer to adjacent care paths for older patients, such as other fractures or elective joint replacement, so each new care path starts from a validated base.

### Network Loop - 4/5
**What you capture today:** Data from every hospital on the same EHR, in the same structure, with no mapping between systems.

**How it compounds:** Each hospital that joins enlarges the cohorts for all others, makes rare profiles usable, makes readmissions in another hospital visible, and makes the benchmark ("how does our practice compare?") more meaningful. Not a 5: every hospital must agree to pool, and the network stops at the boundary of our EHR.

**Total Flywheel Score: 10/20**

**Weakest Loop:** Preference (1/5) — but it is the least important loop for this product.

**Fix for weakest loop:** Keep Preference low on purpose and fix Correction (2/5) first, because it is where a competitor would attack: anyone with the data can build cohorts, but not cohorts that clinicians across many hospitals have confirmed as comparable. Add a "not comparable" flag with a reason on every stay and cohort, review the flags with clinicians each quarter, and turn them into versioned similarity rules shared across the network.

---

## Encroachment Threat Assessment

### 1. Platform Encroachment
**Attacker:** OpenAI ChatGPT (and other consumer health models)

**Vector:** A clinician describes the patient in a free consumer app and asks how such patients are usually treated and how they do. The answer comes from literature and guidelines, not from local data.

**Time-to-threat:** Now — already available.

**% of value at risk:** ~15%, estimate — only the explanation layer; the local, pooled outcomes cannot be copied.

### 2. Vertical Competitor
**Attacker:** Epic (Cosmos / CoMET)

**Vector:** Hospitals that move to another EHR take their data out of our network. Epic already runs the pooled-network model at a far larger scale and uses it to forecast length of stay and readmission.

**Time-to-threat:** 12–36 months, following EHR contract renewal cycles.

**% of value at risk:** ~80% per hospital that leaves, estimate — and every departure weakens the network for the hospitals that stay.

### 3. Adjacent Expansion
**Attacker:** Microsoft Fabric healthcare data solutions

**Vector:** A hospital's data team exports EHR data, maps it to OMOP and builds cohorts itself. Hospitals that cooperate in a hospital network could pool data in a shared platform, across EHR vendors.

**Time-to-threat:** 6–18 months for large hospitals with strong data teams.

**% of value at risk:** ~40%, estimate — the analysis for one hospital or one hospital network; not the full network on our EHR.

---

## 90-Day Encroachment Plan

*Your partner played the Big Tech attacker. What was their plan to kill you?*

**Attacker:** Microsoft (Fabric + Copilot)

**Attack vector (target the weakest loop):** Correction, the weakest loop that matters (Preference scores lower, but there is nothing to attack there) — our "comparable patients" are a technical selection that nobody has validated, so a well-built cohort on a generic data platform looks just as credible.

**Weeks 1-4 - what they ship:** A ready-made "care path variation" template for hip fracture on their healthcare data platform: cohort builder on OMOP data, a dashboard, and a Copilot that writes the summary.

**Weeks 5-8 - how they poach users:** They offer it to hospital networks as a shared data platform, with migration support and cloud credits; data teams like it because it works across EHR vendors.

**Weeks 9-12 - why users don't come back:** Once several hospitals pool data in that platform, the benchmark no longer depends on one EHR, and the data team owns the analysis instead of the EHR vendor.

**Your defense:** Make comparability the product: clinically validated similarity rules, built from reviewer flags across all hospitals on our network, which a generic platform has to rebuild from scratch. Use the advantages that exist by default — one data model, no mapping, outcomes updated with every discharge — and put the view where decisions happen: the care path committee now, the physician later. Build the governance with the hospitals (pooling agreement, no hospital named to another), so joining is easy and leaving means losing the benchmark. Do not fight interoperability: offer an export to OMOP ourselves, so data teams can still do their own research while the validated view stays with us.
