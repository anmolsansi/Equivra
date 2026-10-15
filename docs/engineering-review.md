# Equivra — Engineering review

Target: approved Equivra payments workbench design and PRD. Report destination: this file. No implementation edits authorized.

## Scope record

Feature answers: retained D8/D10/D11/D12 scope; no cuts proposed. Structure: Original arrangement, D14 A. Accepted scope: one backend codebase with API and worker entry points, React UI, PostgreSQL; all exact-money/source/replay/review/snapshot/security/envelope requirements retained. Estimated application change exceeds8 files; no extra service or class hierarchy introduced. Scope accepted as-is. Pending technical source/runtime definitions are architect-owned design work; user product behavior remains fixed.

## Original target baseline — unchanged PRD

# PRD: Equivra

Status: approved-product-scope transcription; detailed engineering contracts pending.
Authority: founder decisions D2–D12 and [approved design](designs/equivra-payments-workbench.md).
Priority: portfolio first, business validation alongside. Capacity: 10 hours/week.

## 1. Problem

A reviewer needs to explain a selected difference between processor, bank and accounting records without inventing missing financial evidence. Equivra's first release demonstrates that workflow with explicitly synthetic data and proves exact arithmetic, source lineage, repeat-safe processing, safe concurrent review and reproducible reports. It does not establish demand for a paid accounting product.

## 2. Users

- Local reviewer: the founder or a viewer using the local synthetic demonstration; imports supported source bundles, investigates, records dispositions and freezes reports.
- Maintainer: starts/stops the local API/worker/database, controls the temporary access code and exercises documented recovery. Not a separate in-product administrator role.
- Bookkeeping firm: potential future buyer hypothesis, not an existing customer or V1 permission role.

## 3. Goals

1. Complete a local import-to-reviewed-report journey using processor, bank and accounting evidence.
2. Trace every displayed financial fact to immutable source records or a documented deterministic calculation.
3. Reject ambiguous or unsupported conclusions, repeated-import duplication and stale decision overwrites.
4. Recreate a frozen report's facts and evidence after source correction and processing recovery.
5. Produce a clean, reproducible portfolio walkthrough with measured limitations and honest synthetic-data labeling.

## 4. Non-Goals

Real financial data, public hosting, SaaS accounts/tenant management, payment movement, journal posting, tax/accounting certification, chargeback submission, fraud detection, live bank/Stripe/accounting connectors, general-ledger replacement, universal CSV/PDF/OCR support, multiple currencies, AI drafting/model calls, an agent framework, or unmeasured production-scale claims.

No rejected business hypothesis is implemented merely to create a reusable platform. No publication, deployment or customer outreach is authorized by this PRD.

## 5. V1 Scope

1. **MAS-1 — Local access:** application data/actions require the current per-start access code. Invalid, missing and previous-start access fail. Retain loopback-only, exact Host and browser-origin protections. No password database or account system.
2. **MAS-2 — Source bundle:** accept exactly the documented Stripe automatic-payout, synthetic bank and synthetic accounting source kinds for the selected synthetic workspace/account and USD. Each file supports up to 10,000 data rows and 10 MiB; reject either exceeded bound visibly. Preserve original values, file/row lineage and input/mapping versions.
3. **MAS-2 — Preview and correction:** display source/field validation issues before treating a revision as runnable. A correction submits the complete three-file bundle as a new immutable revision; unchanged replays must not duplicate economic results. Prior evidence/reports survive.
4. **MAS-3 — Investigation:** process an accepted pinned revision with durable jobs, show queued/running/retrying/failed/completed state, publish no partial result as complete, and recover repeat-safely after interruption.
5. **MAS-3 — Findings:** produce source-linked supported facts, incomplete evidence and ambiguous relationships. Demonstrate partial refunds, dispute withdrawal/reversal, cross-period settlement evidence, identical-amount ambiguity, and a processor refund missing from the supplied accounting export. Equal amount alone cannot resolve a relationship.
6. **MAS-4 — Review:** inspect evidence and record an explicit disposition against the expected case version. Reject stale writes without replacing the newer decision. A review conclusion does not change source amounts or certify reconciliation.
7. **MAS-5 — Freeze/export:** separately freeze the exact selected run and review versions into an immutable workpaper snapshot, retaining unresolved labels. Reject stale freeze requests atomically. Render HTML/CSV from the frozen snapshot; later changes need a new version and freeze.
8. **All MAS — Verification/operation:** behavior-owning tests, safe escaped output, sanitized correlated diagnostics, a clean local setup and documented recovery/reproduction are part of the relevant behavior, not postponed testing work.

## 6. Future Scope (V2+)

AI explanations, hosting, read-only connectors, real-data pilots, multiple users/currencies and commercial billing remain unapproved future decisions. No implementation depends on their hypothetical future shape.

## 7. User Flows

### First local session

1. Maintainer starts the local application using the documented setup.
2. Reviewer opens the UI and enters the current startup code.
3. Valid access reveals the synthetic workspace; invalid or previous-start access reveals no application data.

### Import and investigate

1. Reviewer selects all three supported source files and reviews the source scope.
2. System validates source types, values, limits and required fields; errors identify the source and issue.
3. Accepted input becomes an immutable revision and queues its investigation.
4. Reviewer sees durable processing status, then the revision's case list and coverage diagnostics.

### Review and export

1. Reviewer opens a case and inspects processor, bank and/or accounting row references.
2. Reviewer saves a disposition against the displayed version; a stale request fails visibly.
3. Reviewer freezes the selected reviewed workpaper; changed versions require refresh rather than silent capture.
4. Reviewer downloads HTML/CSV based only on that snapshot, including unresolved labels.

### Correct and recover

1. Reviewer submits a corrected complete source bundle; the old revision remains intact.
2. New processing belongs only to the new revision; old worker completion cannot replace it.
3. If processing is interrupted, its durable status permits safe retry/recovery without duplicate publication.
4. An earlier frozen report still reproduces its original facts and source references.

## 8. Roles & Permissions

| Action | Local client without valid access | Reviewer with current valid access | Worker |
|---|---|---|---|
| Load public UI shell/access prompt | Yes; no application data | Yes | N/A |
| Read runs/cases/evidence/reports | No | Yes, correct owning revision | Internal pinned job access only |
| Submit complete bundle | No | Yes, within documented boundaries | No browser upload role |
| Request eligible processing/retry | No | Yes, validated repeat-safe request | Executes durable owned job |
| Save review / freeze | No | Yes, expected-version enforcement | No authority to invent review decisions |
| Generate export from frozen snapshot | No | Yes | May execute pinned export job |
| Change financial source facts in place | No | No | No |
| Move money/post accounting entries | No | No | No |

Worker DB credentials are internal local configuration, not a user role. A code does not protect against a compromised laptop, provide tenant isolation, or authorize public exposure.

## 9. Data Model (conceptual)

| Entity | Key facts and relationships |
|---|---|
| Synthetic workspace/source account | Single supported workspace/account and USD; no inferred real customer identity |
| Bundle revision | Pins exactly three immutable source versions and declared evidence scope; owns processing lineage |
| Source file/row | Original bytes/values, generated storage identity, source kind, row location and version |
| Investigation run/job | Pinned bundle, rule version, durable state and owned publication |
| Financial relationship/case | Exact supplied amounts, supported reference links, unresolved reasons and evidence scope |
| Review revision | Case identity, expected/new version, allowed disposition and auditable local reviewer action |
| Frozen snapshot/export | Fixed input/run/rule/review versions, facts, evidence links and unresolved labels; exports cannot consult mutable latest values |

Exact schema/IDs, constraints, adapter fields and sign/date semantics are the architect's responsibility before builder packets.

## 10. APIs (conceptual)

Local access validation; complete-bundle upload and preview; revision/run status; investigation request and eligible retry; bounded case listing; evidence retrieval; expected-version disposition; expected-version freeze; frozen snapshot retrieval/export. Exact routes, request/response schemas, status/error codes, replay keys and fixture contracts must be frozen in the orchestration.

## 11. Frontend Requirements

- Access prompt: labeled code entry, invalid-access feedback, restart/reconnect behavior; no data before access.
- Bundle screen: three required sources, explicit formats/limits/scope, validation progress and source/row errors.
- Run/case screen: persistent job state, bounded paging, zero-case coverage explanation, visible incomplete/ambiguous states and failures.
- Evidence/review screen: source references, exact amount/currency/date distinctions, escaped text, retained draft note on conflict, saved version feedback.
- Workpaper screen: draft versus frozen state, selected version, unresolved labels, stale-freeze feedback and recoverable export failure.

Desktop-first with stacked narrow-screen panels, semantic forms/tables, keyboard/focus behavior, non-color-only status, readable long values and accessible status/error announcements. The rough sketch is a workflow reference, not a finished design system.

## 12. Backend Requirements

One TypeScript backend codebase with API and worker processes, PostgreSQL persistence and immutable local source storage. Deterministic domain rules own money and relationships. Durable job/state publication, exact source ownership, validated inputs, safe output, request/job diagnostics and migration/recovery guidance are required. No live external API or model call is needed. Numeric processing timeouts, retry schedule, field bounds and connection pools must be specified in the engineering contract within the approved workload envelope.

## 13. Micro-Architecture Systems

| System | Purpose / covered scope | Dependencies |
|---|---|---|
| MAS-1 Access and local runtime | Local service boundary, startup access, safe configuration | Foundation configuration; consumed by all browser API operations |
| MAS-2 Source bundle ingestion | Preview, validation, immutable lineage, repeat/correction semantics | MAS-1, shared domain/source contracts, DB/storage |
| MAS-3 Investigation and jobs | Exact normalization, supported relationships, unknowns, durable recovery | Pinned MAS-2 bundle; domain/DB/job contracts |
| MAS-4 Evidence review | Read evidence, save versioned auditable decisions | MAS-3 run/case contract and MAS-1 access |
| MAS-5 Workpapers | Atomic freeze, immutable facts and repeatable HTML/CSV export | MAS-2 lineage, MAS-3 run and MAS-4 review versions |

These systems are ownership seams inside one application, not separate services or necessarily separate packages. Tests and diagnostics travel with each system.

## 14. Success Metrics

- All nine approved design acceptance criteria pass with recorded verification artifacts.
- The documented source envelope accepts valid boundary input and rejects either exceeded limit without truncation.
- A clean local environment completes the synthetic walkthrough with documented commands and no paid API keys.
- Actual processing duration, memory and dataset/hardware are recorded before any portfolio performance claim.
- Business observations, if collected, report specific workflow feedback; revenue, repeat use and time saving remain unverified until actually observed.

## 15. Risks

Financial meanings can be wrong despite valid CSV/JSON; authoritative source contracts and expected scenario outcomes must precede implementation. At-least-once jobs can duplicate results without guarded commits. Local browser access needs explicit enforcement. Mutable review/source lookups can invalidate frozen workpapers. The 10-hour weekly capacity makes unbounded UI/infrastructure work expensive. Financial domain rules, concurrency, access and report immutability require architect review rather than builder improvisation.

## 16. Open Questions

No unanswered founder product choice remains in this PRD after D12 A. Upstream engineering must still establish supported source schema/sign/date/state semantics, concrete API/DB/job contracts, local credential transport, runtime/library versions, and actual verified commands. Those are architect-owned design tasks, not missing customer requirements to invent during implementation. Business buyer/data/price hypotheses remain unknown and do not gate the first synthetic portfolio demo.

## Review evidence and limits

Reviewed the approved design, PRD, synthetic scenarios, architecture, ten contracts and twelve packets. Repository baseline is README-only at aaf4eb3; no existing callers, tests, migrations or provider implementations can establish runtime correctness. Proposed source paths are CREATE paths. No observed application bug is claimed. The original PRD above is preserved unchanged.

## 1. Architecture review

**ENG-A1 — Source semantics needed before financial code (confidence10/10, P1).** Motivating requirement: PRD.md:144, “authoritative source contracts and expected scenario outcomes must precede implementation.” The earlier design did not fix columns, signs or matching rules. Disposition: architecture sections4/9 and C-SOURCE/C-DOMAIN now specify exact headers, USD integer cents, direct references, supplied-scope limits, unsupported categories and incomplete/ambiguous cases. TASK-02/TASK-06 must prove S1–S8; no live connector compatibility is claimed. This resolves the written-definition portion of CEO-SOURCE-01; executable proof remains a gate.

**ENG-A2 — Atomic ownership must cover every replay/race boundary (confidence10/10, P1).** PRD.md:35 requires “unchanged replays must not duplicate economic results”; PRD.md:39 requires stale freezes rejected atomically. Disposition: C-DB/C-JOBS/C-IMPORT/C-REVIEW/C-REPORT specify unique content/run/request identities, immutable source durability before DB acknowledgement, same-transaction enqueue and guarded publication, run-row lock ordering for review/freeze, and frozen-payload-only export. TASK-03/05/07/08/09/11 prove both lock orders and before/after-commit interruption with real PostgreSQL. pg-boss documented capabilities are design evidence; installed-version transactional, retry, retention and role behavior are unverified and must stop an incompatible implementation.

**ENG-A3 — Compose and loopback binding need distinct scopes (confidence10/10, P1).** PRD.md:33 requires “loopback-only, exact Host and browser-origin protections.” An internal container listener bound to127.0.0.1 cannot serve normal Docker port forwarding. Disposition: host-native listener127.0.0.1; fixed container listener0.0.0.0 only inside its network; Compose host publication exactly127.0.0.1:4310:4310. Host/Origin/Bearer checks remain mandatory; no arbitrary public-bind setting. Updated architecture, C-FOUNDATION/C-ACCESS and TASK-01. TASK-01/04/12 must verify actual exposure and restart revocation. This is a local runtime realization of D11, not permission for hosting.

Boundary diagram:

```text
browser -> host127.0.0.1:4310 -> fixed Compose port -> API access boundary
upload -> durable immutable bytes -> DB(bundle + run + queue) commit ->202
worker -> pinned bundle -> deterministic facts -> owned result + queue completion commit
review -> lock run -> expected case version -> decision + aggregate version commit
freeze -> same run lock -> expected aggregate -> copy all facts/evidence/decisions commit
export -> frozen payload only -> escaped HTML / formula-safe CSV
```

## 2. Code quality review

No existing application duplication, framework pattern, function size or error-swallowing defect can be observed. Proposed modules are small ownership seams in one backend, with pure financial functions in shared/. Native validation, parameterized SQL and a single Node test runner avoid extra frameworks. No base classes, repository abstraction, event bus, AI adapter or cache is needed.

One concrete shared helper is justified: canonicalJson has three planned consumers (bundle identity, request replay, snapshot hashing) with identical JSON ordering rules. TASK-01 owns it and one unit suite. This is planned net growth, not an invented deletion or LOC saving; no public reusable library is proposed. Money parsing and deterministic investigation each have one owner and are reused by API/worker/report consumers. Full copied contracts in packets are intentional handoff documentation; registry.json is their authoritative source. No new Code Quality findings or tasks.

## 3. Test review

**ENG-T1 — Cross-boundary requirements need explicit behavior-owned checks (confidence10/10, P1).** PRD.md:120 requires durable publication, validation and safe output; PRD.md:39 requires immutable freeze. No tests exist. Disposition: packet-specific assertions and the test plan below cover pure rules, real PostgreSQL/API races, actual browser interactions and recovery. They are requirements, not reported passing tests. Integration seams cannot be replaced by mock-only success.

```text
source bytes -> valid? --no--> bounded diagnostic; no runnable partial bundle
                  |yes
             same content? --yes--> original bundle/run
                  |no
             new pinned run -> crash before commit? -> rollback/retry
                  | completed
             evidence cases -> review expected version? --no-->409 + draft retained
                  |yes
             freeze expected aggregate? --no-->409 + refetch
                  |yes
             frozen payload -> later correction -> old facts unchanged
```

| Suite / owner | Required assertion | Value card |
|---|---|---|
| source/money unit — TASK-02 | Exact cents; negative refund; unsupported/duplicate/malformed inputs; exact10,000/10MiB and one-over rejection | protects=financial facts/input boundary; fails_when=rounding, identity loss or truncation; why_new=no source code/tests exist; seam=none |
| investigate unit — TASK-06 | S1–S8 direct-reference relationships; equal amount does not imply identity; missing observed amount remains null; supplied-scope labels | protects=evidence truth; fails_when=missing evidence becomes a supported conclusion; why_new=new rules; seam=none |
| real storage/import/job integration — TASK-03/05/07 | Transaction rollback, content replay, both interruption sides, stale claim, current-job retry and immutable grants | protects=durable ownership; fails_when=duplicate/partial result or accepted dangling files; why_new=real transactional boundary; seam=disposable local PG and explicit interruption barrier |
| review/snapshot integration — TASK-08/09 | Both review/freeze lock schedules; stale expected versions; identical replay; all-case snapshot; prior snapshot after correction/review | protects=review/report consistency; fails_when=mixed versions or later lookup changes frozen facts; why_new=cross-module contract; seam=two real DB connections with explicit barrier |
| access/report boundary — TASK-04/09/11 | Missing/old code, hostile Host/Origin, role denial, escaped HTML, CSV formula text, no source/code in diagnostics | protects=local data and safe output; fails_when=unauthorized access or executable source text; why_new=security boundary; seam=real API/output bytes |
| browser journey — TASK-10/12 | Import→evidence→review→freeze→download; pending/error/empty/stale states, code re-entry, keyboard and narrow screen | protects=usable portfolio journey; fails_when=user cannot recover or exported facts diverge; why_new=browser-only interactions; seam=actual local providers |
| restore/envelope integration — TASK-12 | Paired DB+files restore preserves hashes/facts; mismatched archive rejected; workload bound observed with recorded hardware/time/memory | protects=recovery and truthful claims; fails_when=history lost or unsupported performance claimed; why_new=operational acceptance; seam=disposable local resources |

Tests made obsolete: none. No LLM behavior/eval is in scope. Use Node native runner, with Playwright as a browser library under that runner. Do not test trivial wiring or mirror implementation internals. All proposed command strings remain unverified until G0.

## 4. Performance review

**ENG-P1 — Approved input envelope needs bounded processing, not a speed promise (confidence10/10, P1).** PRD.md:34 fixes10,000 rows/10MiB per source; PRD.md:120 requests numeric runtime bounds. Disposition: streaming input caps, bounded fields/errors/previews, indexed exact-ID maps, paged case queries, indexed FK/identity lookups, one heavy worker, explicit SQL/lock/upload/job deadlines and finite retry policy. At most30,000 source rows/30MiB original file bytes per bundle; normalized/JS/DB overhead is unknown until measured. Avoid SQL per row in relationship loops and unbounded API responses. No cache or parallel workers required. TASK-12 records timing/memory on named hardware; it must not invent a response-time SLA or call a timeout setting measured capacity.

## Decision ledger

| ID | Disposition and authority | State |
|---|---|---|
| ENG-SCOPE | D14 A retains original application arrangement; D9 HOLD SCOPE | Accepted prior answer |
| ENG-A1 | Architect-owned source definitions under explicitly invoked project-orchestrator; preserves D7/D10 and PRD financial evidence behavior | Written remedy complete; provider proof pending |
| ENG-A2 | Architect-owned transaction/identity contracts under orchestrator; assertions preserve D10 and approved freeze/replay acceptance | Written remedy complete; provider proof pending |
| ENG-A3 | Architect-owned fixed Compose realization of D11 loopback/Host/Origin boundary; no hosting | Written remedy complete; local exposure proof pending |
| ENG-T1 | Exact approved regression requirements mapped to packets; no new user behavior | Written requirements complete; tests not implemented |
| ENG-P1 | Architect-owned bounds within D12 envelope; no speed SLA | Written remedy complete; measurement pending |

Approval readiness: PASS for written planning dispositions ENG-SCOPE, ENG-A1/A2/A3/T1/P1, with the actual authority references above. This is not execution or release readiness. No new founder product decision is being silently accepted. Existing D13 A already selects engineering review followed by orchestration; no duplicate navigation question is needed.

## Outside Voice

Installed eng-review preflight returned under_codex. Its configured Codex outside reviewer is this host, so no outside process started. Required native fallback capabilities (declared Plan type, TaskOutput and TaskStop) are unavailable. No general-purpose substitute was launched. Status unavailable; zero external findings and zero independent agreement credit. Suggested tooling repair in the skill is setup --host codex; live skills were not modified. The earlier CEO phase separately attempted Claude and failed API DNS resolution; that does not count as engineering coverage.

## What already exists and what is outside scope

Existing README/repository metadata and approved planning artifacts are reused. There is no application to refactor. Explicitly excluded: live connectors, real financial/customer data, cloud hosting, paid subscriptions, AI explanations, multi-user accounts, marketing outreach and universal accounting format support. These already have scope dispositions; no speculative TODO file or extra feature is added.

## Failure modes and recovery

| Path | Failure and visible result | Required proof |
|---|---|---|
| Local start/access | Wrong runtime/config or hostile access: fail startup or safe401/403; no app data | TASK-01/04 plus host port inspection |
| Source acceptance | Invalid/oversize input or storage failure: bounded4xx/5xx; no runnable partial bundle; preserve accepted files | TASK-02/05 rollback and exact-bound fixtures |
| Queue/run publication | DB error/crash/lost owner: rollback or retry/failed state; no duplicate facts | TASK-07 real commit-boundary interruption |
| Review/freeze | Stale/racing expected version:409 with recoverable refetch; no mixed snapshot | TASK-08/09 both lock schedules |
| Report download | Render/storage failure: safe error/retry from same snapshot; unsafe text inert | TASK-09/10 exported byte assertions |
| Restore | Missing/mismatched archive: stop with integrity error; preserve existing history | TASK-12 disposable paired restore |

Failure modes: 0 critical gaps flagged as unhandled/silent in the written plan. Every named failure has handling and a proposed check; none has executed. Inline flow comments belong in future jobs/reviews/reports implementation where commit and lock ownership are otherwise unclear.

## Implementation Tasks

- [ ] **T1 / TASK-01/02/06 (P1)** — From ENG-A1/A3: establish verified local baseline and exact source/rule fixtures. Owned files, acceptance, rollback and commands are in the linked packets.
- [ ] **T2 / TASK-03/05/07/08/09/11 (P1)** — From ENG-A2: implement and prove revision ownership, real transaction/replay/race behavior and immutable workpapers.
- [ ] **T3 / TASK-04/10/12 (P1)** — From ENG-A3/T1/P1: prove local access, full browser journey, workload envelope and paired restore.

These group the twelve packet outcomes without adding tasks. Serial packet estimates total166h. Human versus AI-assisted duration remains unmeasured; no unsupported acceleration ratio is used as a delivery promise. TASK-01/02 results should drive the next estimate.

## Workstreams and integration

The exact file ownership and66 edge start/merge/runtime dependencies are in orchestration.md and tasks/index.json. Possible lanes: Sources / Storage / Access after foundation; then Domain / Ingestion / Review / Web against frozen fixtures; Jobs / Reports; API convergence; browser convergence; local release. Shared app/main/worker/App files are serialized by predecessor ownership. The current single10h/week operator follows the merge order; no agent, worktree or parallel dispatch is authorized by this plan.

| Modules | Prerequisite / merge gate |
|---|---|
| Foundation | Implementation authorization, then G0 command/runtime evidence |
| Sources / Storage / Access | Foundation; Storage merges after source conformance |
| Domain / Ingestion / Review / Web | G0 and frozen consumed contract/fixtures; actual provider checks before merge |
| Jobs / Reports | Domain/DB and review/source contracts as listed in packets |
| API convergence | INT-01 plus access/review/reports; INT-02 real API proof |
| Browser convergence | INT-02 plus Web; INT-03 real browser proof |
| Local release | All checkpoints plus recovery/envelope/runbook evidence |

## Completion summary

Written engineering review and orchestration are complete with concerns. Four-section findings:5 (Architecture3, Code Quality0, Tests1, Performance1), all mapped to written remedies and implementation gates. Unresolved new founder decisions0; unhandled critical failure gaps0; outside coverage unavailable. Saved plan is not Eng CLEAR: issues_found includes mapped findings and real evidence is absent. CEO-SOURCE-01 and CEO-RUNTIME-01 now have written definitions, while their source/provider/command conformance portions remain pending. No implementation clearance, passing test result, CI, publication or deployment is claimed.

## Suppressed findings

No hypothetical framework, scaling, LLM, multi-tenancy or monetization findings were promoted. No claims of existing bad code or measured performance were made. Provider documentation is not installed-library proof.

## Saved verification artifacts — completed 2026-10-15

QA plan saved and read back at `/Users/mac/.gstack/projects/anmolsansi-Equivra/mac-main-eng-review-test-plan-20261015-061955.md`; three review task groups saved in `tasks-eng-review-20261015-061955.jsonl` in the same folder. These contain future acceptance requirements, not passing runtime results.

Static validation passed for10 contracts/20 fields each,12 packet-required sections, all copied contract content, every provider-consumer edge,66 edge metadata records, acyclic16-node merge DAG,3 checkpoints, same-wave write disjointness, packet sizing, existing local Markdown links, sample decimal arithmetic and final report structure. Generated source/wire examples remain design fixtures. Original snapshot sample is explicitly a subset illustration, not a complete computed report. No application build/tests, Docker daemon/provider compatibility, browser acceptance, envelope benchmarks or recovery were run.

## GSTACK REVIEW REPORT

| Review | Trigger | Why | Runs | Status | Findings |
|---|---|---|---|---|---|
| CEO Review | plan-ceo-review / D9 HOLD SCOPE | Scope and strategy | 1 repo-local; helper history absent | DONE_WITH_CONCERNS | Two technical prerequisites now specified in writing; executable conformance pending |
| Outside Review — CEO | Claude CLI | Independent CEO challenge | 1 attempted | unavailable | API DNS error; no completed critique |
| Eng Review | plan-eng-review / D13/D14 | Architecture and tests | 1 | issues_open (PLAN) | 5 mapped findings,0 unhandled critical gaps,0 new founder decisions |
| Outside Review — Eng | Configured Codex preflight | Independent engineering challenge | 0 executions;1 preflight | unavailable | Own-harness mismatch; required bounded fallback unavailable |
| Design Review | plan-design-review | UI quality | 0 | NOT RUN | Office-hours spec review9/10 is a separate review |
| DX Review | plan-devex-review | Developer experience | 0 | NOT RUN | Clean setup remains TASK-12 evidence |

**OUTSIDE COVERAGE:** CEO/Claude unavailable; Eng/configured Codex unavailable. No cross-model completion or agreement credit.

**VERDICT:** Complete written plan; not cleared for unrestricted implementation delegation or release. Eng review required at executable conformance; G0 and provider/integration checks remain.

**UNRESOLVED DECISIONS:**
- CEO-SOURCE-01: written source semantics supplied; owning source/domain/provider conformance still pending implementation.
- CEO-RUNTIME-01: written runtime/API/DB/job contracts supplied; selected-runtime commands and installed-library transaction/recovery/access behavior still unverified.
