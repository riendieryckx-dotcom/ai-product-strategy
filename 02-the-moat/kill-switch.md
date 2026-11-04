# Kill Switch Audit

## Vendor Dependency Assessment

| Dimension | Current State | Risk Level | 48-Hour Action |
|-----------|--------------|------------|---------------|
| **Provider** | Google Gemini on Vertex AI (EU region) for both tasks; Google is also our cloud provider. The model sees patient record content and is part of the certified device, so any model change needs validation. A scripted fallback keeps the history findings working. | H | Pin the model versions in the technical documentation. Start validating an open-weight standby that runs on Vertex AI and on our on-premise OpenShift. Have legal and the DPO confirm Google as sub-processor: EU region, no training on hospital data. |
| **Abstraction** | One call site in the prototype (`runAI()`, prompt inline in `prompt()`), on the claude.ai runtime; production calls Gemini. No interface. | M | Put the calls behind `dxGateway.selectFindings()` and `dxGateway.suggest()`, with the provider in config, the prompt in `prompts/dx-suggestions.v1.txt`, and the grounding check in the gateway for every provider. |
| **Routing** | One model, one call; the Module 3 cascade exists on paper only. | M | Flash-class on every new result; Pro-class when the findings change, a result is out of range, a severity of 40% or more is possible, or the physician asks. On error or after 10 s, show the last valid list. Log provider, version, latency and cost. |
| **Eval** | 35 golden rows on paper and no automated run, so the standby cannot be proven. | H | Automate the golden suite in `evals/golden/` for Gemini and the standby. Gate: 100% on the safety rows (7, 8, 9, 13, 14, 21, 35), top 5 ≥85%, no severity underestimate of more than 10 points on severity 3–4 cases. |

## Portability Score
**Partial.** The value is ours: the record, the selection of findings, the calibration and the certification file. But a certified device can only switch to a standby validated in advance, and today there is no standby, gateway or automated eval. With them the score becomes **Ready**: ready for the standby, not for any new model.

## If Google doubles pricing tomorrow:
Small impact: inference is about €87 of €2,047 per hospital per month, so the gross margin moves from about 71% to about 70%. A rise in hosting prices weighs more (infrastructure is €500).

- **Hour 0–4:** keep more updates on the Flash-class model (the 40% severity rule stays) and reuse lists until the findings change.
- **Hour 4–24:** rerun the golden suite on the validated standby, on Vertex AI and on-premise.
- **Hour 24–48:** if it passes, plan the switch for the next release, on-premise if hosting is the problem; if not, stay and accept the price. An unvalidated cheaper model is never an option.

## If Google ships a competing product:
Google already builds medical models, so this is realistic. What it cannot copy:

- **The record and its updates**, including letters from other hospitals through the eHealth exchange. Google sees only what one call sends and may not train on it.
- **Calibration on confirmed outcomes**, per hospital.
- **The certified status** and the quality system behind it.
- **The place in the workflow** and the agreements with hospitals.

Because Google is both model and cloud provider, the standby must run on-premise: the gateway lets us leave Google for both.
