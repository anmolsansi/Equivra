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
