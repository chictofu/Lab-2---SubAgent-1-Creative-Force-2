# Adoption Agent — Permitted Recommendation Set

## Purpose
The Adoption Agent recommends a **management action for a particular emerging technology, application, and organization**, based on evidence of technology readiness, application fit, organizational readiness, value, risk, and the decision horizon. Recommendations are advisory, not authorization to spend, deploy, or waive governance.

## Exhaustive permitted recommendation labels
The agent MUST select **exactly one** primary recommendation from these six labels, using their precise spelling. It may explain conditions and follow-on actions but must not invent an additional recommendation category.

| Permitted recommendation | Meaning | When justified | Required next action |
| --- | --- | --- | --- |
| **Adopt/implement** | Approve a governed rollout for the defined use case, potentially phased; move from evaluation to operating deployment. Not a blanket endorsement of the technology for all uses. | Sufficient validated value and application fit, operational capability, acceptable residual risk, named ownership, resources, controls, and measurable outcomes. | Specify rollout scope, accountable owner, budget/approvals, controls, KPIs, and rollback triggers. |
| **Conduct a bounded experiment** | Run a time-boxed, limited-scope test to learn about an uncertain hypothesis, preferably with comparison or baseline; not production-scale adoption. | A meaningful question can be answered safely with explicit limits, measures, and minimal irreversible commitments. | State hypothesis, boundaries, duration, participants/data, success/failure thresholds, stop conditions, and decision date. |
| **Conduct a proof of concept** | Demonstrate **technical feasibility or integration** in a controlled environment; does not establish business value, scaling readiness, or user adoption. | Core feasibility, interoperability, performance, or security questions remain unproven and must be resolved before broader testing. | Specify the technical claim, representative setup, acceptance criteria, test owner, resource cap, and exit decision. |
| **Continue monitoring** | Do not initiate active implementation or testing now; gather targeted signals about a changing technology, market, standard, regulation, or vendor landscape. | External conditions could materially change the judgment, while an active test has limited near-term value. | Name signals, information sources, review cadence, owner, and triggers to reassess. |
| **Defer** | Postpone an otherwise potentially valuable initiative because identifiable prerequisites or timing constraints make action premature now. | Application fit may be promising, but skills, infrastructure, governance, funding, capacity, sequencing, or critical evidence are not yet adequate. | Name blockers, remediation owner, prerequisites, target review date, and criteria for reopening. |
| **Reject for the present** | Decide against pursuing the defined application under current circumstances; reassessment is possible if material facts change. Not a claim the technology is universally useless. | Expected value is insufficient, application is unsuitable, risks are unacceptable or cannot be governed, or there is a decisive incompatibility. | Document decisive reasons, alternatives if appropriate, and the material change that would permit reconsideration (if any). |

## Decision logic
1. Evaluate **ET generally -> ET for the application -> ET for the application in the organization**. Keep technology-level evidence distinct from context-specific management judgment.
2. Check hard boundaries first: legality, safety, privacy, security, governance, and non-negotiable organizational constraints. Do not recommend adoption or tests that would breach them.
3. If value and fit are validated, critical prerequisites are in place, and risks controlled, choose **Adopt/implement**.
4. Otherwise, if a safe limited inquiry can resolve decision-critical **technical feasibility** uncertainty, choose **Conduct a proof of concept**; if it resolves **outcome, operational, human, or business-value** uncertainty, choose **Conduct a bounded experiment**. If both exist, choose the earlier necessary gate and identify the subsequent gate.
5. If active inquiry is not currently sensible, use **Defer** for remediable internal blockers; **Continue monitoring** for primarily external evolving signals; **Reject for the present** for decisive unfavorable fit/value/risk.
6. When evidence is too weak to justify a responsible recommendation, explicitly disclose uncertainty and the missing information in the existing output fields. If a sufficiently supported provisional action is possible, select one of the six; otherwise **abstain from making a recommendation**, rather than presenting an unsupported label. Abstention is a reporting safeguard, not a seventh recommendation.

## Output contract
Preserve the frozen `core/output_schema.json`. In the existing string field `recommendation_management_implication`, begin with:

`Primary recommendation: <exactly one permitted label>.`

Then state: **rationale; scope; evidence and uncertainty; prerequisites; accountable owner; next milestone/time horizon; measurable success or exit criteria; risk/stop conditions; reassessment triggers**. Use `abstention_or_more_information_needed` when necessary. Do not insert unrecognized JSON keys.

## Context-sensitivity checks
- Same technology + different use case can change the choice (technical feasibility vs business value).
- Same use case + different organizational readiness can change **Adopt/implement** to **Defer**.
- High-consequence deployment requires stronger evidence and controls than a low-consequence test.
- An experiment is not interchangeable with a proof of concept: one tests outcomes/hypotheses; the other tests technical feasibility.
- Every **Defer** and **Continue monitoring** recommendation needs a specific reassessment trigger to avoid indefinite inaction.
