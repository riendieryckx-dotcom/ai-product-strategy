# Kill Switch Audit

> **Primary vendor:** Google Cloud — the planned production platform for Comparable Patients, supplying the pooled data platform, compute and model access (managed model service, EU region). Anthropic Claude, used in the prototype, becomes one of the models on that platform. The audit describes the planned production architecture; the prototype is the starting point.

## Vendor Dependency Assessment

| Dimension | Current State | Risk Level | 48-Hour Action |
|-----------|--------------|------------|---------------|
| **Provider** | One cloud provider for three layers: the pooled hospital data, the compute for comparability and statistics, and access to language models. The model layer is swappable (several model vendors on the same service); the data and compute layers are not. | H | **Models:** designate one primary model and one warm standby from another vendor; both run in every eval pipeline, and the standby never serves users unless the primary fails the eval or its contract changes. **Data:** schedule a daily export of the pooled dataset to on-premise storage on our existing OpenShift platform, in an open, documented format (Parquet, OMOP-compatible schema), and test one full restore by Friday. |
| **Abstraction** | Comparability and statistics run in our own code; only the committee summary uses a language model. In the prototype that call is hard-coded in one browser function; in production no interface exists yet. | M | Define a backend interface `CommitteeSummaryProvider` (Java 21) with one adapter per model (Gemini, Claude) in a separate adapter package; add a build check that fails when vendor SDK classes are used outside that package. |
| **Routing** | All model calls are planned through one managed model service. Several models are available there, but every route depends on the same cloud provider. The rule-based summary is the only route outside the platform. | M | Write the routing rule in the gateway: default model for normal cohorts, stronger model for small or mixed cohorts, rule-based summary on error or after 15 seconds. Log provider, model version, latency and token cost for every call. |
| **Eval** | No automated tests. We cannot prove that another model, or a new version of the same model, meets the quality bar. | H | Build a golden set of 30 synthetic cohort profiles with automated checks: (1) no treatment recommendation, (2) every number in the summary matches the computed statistics, (3) a selection effect is named when the patient mix differs by more than 15 percentage points between care paths, (4) uncertainty is flagged when the cohort is under 30 or a care path has fewer than 15 stays. Run it in the GitLab CI pipeline on every model or prompt change; go live only with 100% on checks 1 and 2 and at least 90% on checks 3 and 4. |

## Portability Score
**Partial.** The model layer is close to Ready: one task, several models on the platform, and a rule-based summary that keeps the product working with the AI switched off entirely. The data and compute layer is not: today, leaving the cloud provider would mean rebuilding the pooled data platform. With a tested export to on-premise storage, the provider interface and the eval pipeline, the score moves to **Ready** for the model layer and to a documented, tested exit path for the data layer.

## If Google Cloud doubles pricing tomorrow:
- **Model costs (hour 0–24):** Turn on caching in the gateway (same profile on the same data version returns the stored summary), run the golden set on the cheaper models on the platform and on Claude directly through Anthropic's API, and switch the default to the cheapest model that passes.
- **Data and compute costs (hour 24–48):** Measure what doubling means per hospital per year, start the contract discussion, and confirm the latest export restores on-premise. Leaving the cloud in 48 hours is not realistic; the goal is to prove that leaving within a planned migration is possible, so the price negotiation is credible.
- **What we do not do:** move to a cheaper model that fails the eval. A summary that recommends a treatment or misstates a number is not an option at any price.

## If Google Cloud ships a competing product:
A cloud provider could offer hospitals a general healthcare analytics product on its own platform. What it cannot replicate:

- **The pooled network:** structured treatment and outcome data from all hospitals on the same EHR, in one data model, updated with every discharge. It sits in our own tenant, and the contract must exclude any use by the provider for its own products (to be verified with legal before go-live).
- **Validated comparability:** similarity rules confirmed by clinical reviewers across hospitals (the Correction loop). That is our work, not the platform's.
- **The integration in the EHR:** the view is built into the EHR where care path committees and, later, physicians already work: no export, no separate tool or login, and it opens directly from the context of the care path or the patient.
- **The governance with hospitals:** the pooling agreement and the rule that no hospital is shown to another. Hospitals trust that arrangement with their EHR vendor; a cloud provider would have to build it from scratch, hospital by hospital.

Because the same provider would then be both our platform and our competitor, the export path and the provider interface turn from good practice into a requirement.
