# Three-Axis Vulnerability Diagnostic

## Product

**Product:** AI Product Advisor — a portfolio-level decision advisor for product organisations that weighs new requests against objectives, running work and portfolio principles, and keeps the product leader in charge of the decision.
**Your Role:** Product & Strategy lead at a Belgian hospital-software company; owner of this bet and first user (the advisor is tested on our own portfolio).

---

## Scores

### Contextual Moat — 2/5
*Workflow depth × switching cost. Would users leave in a weekend if a competitor showed up?*

**Score rationale:** It sits next to the system of record (Jira, Productboard), not inside it, so users could leave in a weekend until the advisor holds their decision history.

**Named attacker (from partner challenge):** Atlassian Jira Product Discovery + Rovo — AI that works inside the roadmap and ideas the PM already curates. https://www.atlassian.com/software/rovo/connectors/jira-product-discovery

---

### Data Advantage — 1/5
*Proprietary signal that compounds with usage. What do you see that OpenAI doesn't?*

**Score rationale:** Today nothing compounds: no proprietary data, and the decision log is local and per customer; the potential signal (advice → decision → outcome) does not exist yet. Lowered from 2 after the partner challenge.

**Named attacker (from partner challenge):** Productboard Spark — already holds feedback, OKRs, strategy docs and roadmap, and positions itself as an agent that gets smarter every day. https://www.productboard.com/spark/

---

### Platform Exposure — 2/5
*Encroachment risk × pivot speed. If Apple/Google/OpenAI ships your hero feature native — then what?*

**Score rationale:** Synthesising OKRs, estimates and research into advice, including asking clarifying questions, is already native in general agents; pivot speed is high (small product, no legacy), but there is little left to pivot to if the method is copied.

**Named attacker (from partner challenge):** Microsoft 365 Copilot Researcher — reasons over work data and connectors (incl. Confluence), bundled in an existing licence. https://learn.microsoft.com/microsoft-365/copilot/researcher-agent

---

## Top Vulnerability
If the value is better analysis, it is a feature of Copilot, Rovo or Spark; the bet only holds if the value is the portfolio decision method and the decision history it builds.

## Confidence Level
L — the need is real in my own organisation, but nothing yet proves that the method and the decision log beat a general-purpose assistant.
