# Equivra — initial discovery checkpoint

Date: 2026-10-14
Status: discovery/design approved; CEO review recorded with concerns; engineering/orchestration remains incomplete.

## Request

Help turn the supplied opportunity research and AgencyClose proposal into a project plan using the requested product, engineering challenge, CEO review, and orchestration skills. No application implementation requested at this stage.

## Confirmed founder decisions

- Product name: **Equivra**. The founder explicitly rejected AgencyClose as the product name. References to AgencyClose below identify the supplied proposal only.
- Discovery route: guided `/office-hours`, approved by the founder's reply "A" to prerequisite D1. Resume the requested CEO review after discovery.
- Priority: **portfolio first, business alongside**, explicitly selected by the founder. Build a defensible engineering demonstration while testing business demand in parallel. Customer interviews and priced pilot commitments do not gate the initial synthetic-data demo; real customer data and commercial launch require their own readiness checks.
- Discovery uses the office-hours builder route under this priority.
- Capacity: **10 hours per week**, supplied by the founder. Treat calendar estimates as provisional until task sizing; the attachment's 4–6 week full-MVP estimate assumed a higher weekly capacity.
- Workflow: **payments exception investigation**, selected by the founder's reply "A" to D3. Investigate differences across Stripe, bank, and accounting exports. The proposed demonstration centers on refunds, dispute reversals, settlement timing, source evidence, repeat-safe imports, and interrupted-job recovery. This selects the domain; exact supported formats, rules, implementation scope, and architecture remain to be designed.

## Confirmed evidence

- Repository baseline is documented in `docs/repo_context.md`.
- The two supplied documents recommend different primary customers and workflows.
- Live check: https://www.upstaanalytics.com/ advertises invoice extraction, spend/execution matching, client billing validation, and agency audit packs. Vendor advertising establishes overlap, not product quality or customer outcomes.
- Live check: https://docs.stripe.com/reports/payout-reconciliation documents native payout reconciliation. A generic payout-matching feature alone therefore needs a clearer reason to exist.
- No customer interviews, payment commitments, or usable source samples were verified in this session.

## Proposed charter, not approved scope

Explore a narrow financial exception review product that helps an operator trace a discrepancy to source records and export a reviewed explanation. Business outcome: measurable reduction in recurring investigation work with credible purchase intent. Engineering outcome: demonstrable exact financial arithmetic, source lineage, repeat-safe imports, and reproducible reports.

Selected direction: payments exception investigation across Stripe, bank, and accounting exports. Bookkeeping firms are the proposed commercial audience, not a validated buyer segment. Agency advertising billing reconciliation was considered and not selected for the initial project.

## Preliminary recommendation

Build the plan around the selected payments investigation workflow. Prioritize engineering behavior that can be demonstrated and verified with explicitly synthetic data. Test the bookkeeping business hypothesis alongside development without making buyer commitments a prerequisite for the first portfolio demo.

Proposed first proof: one account, one currency, one period, documented CSV formats, explicit unsupported cases, deterministic discrepancy checks, source-linked review, and a reproducible export. AI explanations remain a candidate addition whose value must be compared with rules/templates. Scope, stack, hosting, and delivery dates are not frozen.

## Decision ledger

| ID and owner | Contract and evidence | Current | Proposed | Status | Exact approval and scope |
|---|---|---|---|---|---|
| DISC-01 — founder | D3 compared payments exception investigation with advertising billing reconciliation | Payments exception investigation selected | Define bounded Stripe/bank/accounting export demonstration | approved | Founder replied "A" to D3; selects payments domain, not a stack or exact implementation scope |
| DISC-02 — founder | No DESIGN.md or docs/designs document found; no private project design directory found | Guided discovery approved | Run office-hours before resuming CEO review | approved | Founder replied "A" to prerequisite D1 |
| DISC-03 — founder | No verified buyer access, time, or budget | Unknown constraints | Establish reachable buyer, sample access, weekly capacity and spend ceiling | unresolved | None |
| DISC-04 — founder | Founder reply to D2: "Portfolio first, business alongside" | Portfolio first; business validation alongside | Initial synthetic demo proceeds independently of buyer commitments | approved | Exact founder priority; does not approve a workflow, stack, or commercial launch |
| DISC-05 — founder | Founder answered "10" to hours per week | 10 hours/week | Size demonstrable milestones within this capacity | approved | Weekly availability only; no delivery deadline promised |
| DISC-06 — founder | D5 listed three discovery premises | Synthetic data first; evidence before explanation; reproducible local demo first | Compare implementation approaches within these premises | approved | Founder replied "A" to D5; accepts all three premises, not a frozen feature list or architecture |
| DISC-07 — founder | Optional discovery second opinion offered in D6 | Skipped | Proceed directly to approach comparison | approved | Founder replied "b" to D6; no reviewer ran; later requested review stages remain applicable |
| DISC-08 — founder | Local-first, synthetic-data, portfolio-first premises; 10 hours/week | B: local web investigation workbench | Prepare design using TypeScript API, React UI, PostgreSQL and one worker | approved | Founder replied "B" to D7; selects approach, not implementation, hosted deployment, or exact source contracts |
| DISC-09 — founder | Reviewed design and workflow sketch presented at D8 | Product design approved | Resume requested CEO review, then detailed orchestration | approved | Founder replied "A" to D8; accepts first product slice and success criteria, not implementation authorization |

## Discovery premise checkpoint — approved D5

The founder approved these premises by replying "A" to D5. They guide the design; exact release scope and implementation contracts remain unchosen.

1. The first deliverable is a synthetic-data portfolio demonstration of payments exception investigation. Business discovery runs alongside it; neither a paid pilot nor real financial data is required to complete that first demo.
2. The demonstration's value is traceable investigation and engineering correctness, rather than a claim to replace Stripe reports, accounting software, or an accountant. Rules own amounts and supported relationships; AI, if selected later, drafts evidence-grounded explanations for review.
3. Delivery is staged for 10 hours/week. Begin with a reproducible local demonstration; hosted distribution, real customer data, and commercial operation are separate later decisions with their own readiness requirements.

Research check: Stripe provides native payout reconciliation; public open-source reconciliation engines include Reconify and Settler. These are reference candidates, not audited or selected dependencies. Conventional deterministic matching and explicit exception review remain suitable; no novel market gap is established. There is no existing Equivra application code to reuse.

## D7 — implementation approaches, B selected

Both approaches target documented synthetic Stripe/bank/accounting CSVs, deterministic monetary checks, evidence-linked exceptions, persisted reviewer decisions, reproducible workpapers, and failure/replay verification. Exact source contracts and financial rules remain for architecture planning. AI is a separate later scope decision, not included implicitly in either choice. No live connectors or hosted application is included in this approach selection.

### A — Local command-line investigator (minimum viable approach)

- Summary: TypeScript command-line workflow with SQLite persistence and a generated HTML report; review decisions are recorded through commands.
- Effort: M; initial planning allowance without AI assistance 40–65 hours, with AI assistance 25–45 hands-on hours (roughly 3–5 weeks at 10 hours/week). These are estimates, not a delivery commitment.
- Risk: medium; financial semantics still require careful testing.
- Pros: few runtime components; repeatable scripted demonstration; easy to inspect and debug locally.
- Cons: weaker interactive presentation for nontechnical viewers; later web adoption requires UI and server work; SQLite does not demonstrate PostgreSQL operations.
- Reuses: no existing application code; standard CLI/file workflow and database transactions. Exact libraries and versions remain unselected.

### B — Local web investigation workbench (recommended long-term approach)

- Summary: One TypeScript backend codebase with separate API and worker processes, PostgreSQL persistence, and a small React review interface. Local orchestration; no separately owned microservices.
- Effort: L; initial planning allowance without AI assistance 90–140 hours, with AI assistance 60–100 hands-on hours (roughly 6–10 weeks at 10 hours/week). Re-estimate after scope/contracts and first milestone; these are not quoted delivery dates.
- Risk: medium; integration, UI, and local database setup add work.
- Pros: a complete visual workflow that an interviewer can follow; persistence, concurrent review, durable jobs, and recovery can be demonstrated together; a clearer route to later customer trials.
- Cons: slower first finish than A; more local processes and integration checks; frontend effort can distract from financial correctness.
- Reuses: no existing application code; established modular application boundaries, PostgreSQL transactions, and database-backed jobs. No custom queue infrastructure, Redis, Kafka, Kubernetes, or workflow framework proposed for this first approach.

Recommendation: B because the founder prioritizes a portfolio artifact with a convincing end-to-end demonstration while retaining a route to business use. Build it in demonstrable increments rather than waiting for the complete interface. Choosing A remains a valid faster path if the shorter initial schedule matters more.

## Next sequence

Approved design saved at `docs/designs/equivra-payments-workbench.md`, with a static workflow sketch in `docs/designs/assets/`. Founder approved at D8. The required design spec review ran twice: 2 findings in round 1, both explicitly confirmed resolved in round 2; final score 9/10 and zero unresolved findings. Saved verdicts are in `docs/designs/equivra-review/`. This review is separate from the optional discovery second opinion the founder skipped. CEO review is saved in `docs/equivra-ceo-review.md`; the later engineering/orchestration checkpoint below supersedes the early planning status.

1. Discovery prerequisite and demonstration domain selected; continue guided discovery.
2. Define user problem, measurable outcomes, exclusions, evidence gates, and constraints.
3. Continue the requested CEO review with actual scope decisions.
4. Produce the PRD, architecture decisions, invariants, contracts, dependency graph, task packets, and release gates using the requested orchestrator.

At that early checkpoint no architecture, implementation tickets or contracts existed. See the later checkpoint for the completed written plan and remaining execution gates.

## Subsequent review decisions

- D9 a: HOLD SCOPE.
- D10 A: complete three-file bundles for corrections, retaining prior revisions/reports.
- D11 A: temporary per-start local access code plus loopback/Host/browser protections.
- D12 A: up to 10,000 data rows and 10 MiB per source file, rejecting either exceeded limit without truncation. These are supported-envelope requirements, not measured speed.

## CEO review checkpoint

All eleven CEO review sections and the terminal report are saved in `docs/equivra-ceo-review.md`. Scope remains HOLD SCOPE. Product requirements are transcribed in `docs/PRD.md`; synthetic scenario expectations are in `docs/demo-scenarios.md`. Two architect-owned prerequisites remain: exact financial source contracts and concrete runtime/verification contracts. The external CEO review failed with API DNS error ENOTFOUND and returned no findings; missing coverage is recorded explicitly. No application code, verified test commands, or delegation-ready implementation packets exist yet.

## Engineering and orchestration checkpoint — 2026-10-14

D13 A selected engineering review then orchestration. D14 A retained the original application arrangement after the engineering complexity gate. Product scope remains unchanged. Architecture,10 full contracts,12 bounded packets,66 dependency edges and3 integration checkpoints are saved in architecture.md, contracts/, tasks/ and orchestration.md. Written definitions address the two CEO prerequisites; executable conformance remains pending.

Static packet checks pass: acyclic merge DAG, one-owner provider/consumer records, disjoint same-wave writes and <=3-day packet sizing. TASK-01 owns G0 runtime/command bootstrap; unrestricted downstream delegation is NOT READY until relevant gates pass. No application code, existing test commands, passing runtime/CI evidence, branch, commit or deployment was produced.

Packet sizing refines the earlier rough60–100h allowance to166 engineer-hours, about17 weeks at10h/week before contingency; no measured AI acceleration or promised finish date. Re-estimate after foundation/source work. Engineering findings are mapped to packets; independent engineering coverage is unavailable because of configured own-harness mismatch and missing required fallback capabilities. No live skill or observation memory changed.
