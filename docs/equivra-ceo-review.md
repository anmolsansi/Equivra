# Equivra — CEO review working plan

Status: DONE_WITH_CONCERNS for CEO scope review — HOLD SCOPE; engineering/source contracts remain open and outside review unavailable. Not implementation-ready.
Branch/base: main. Repository: anmolsansi/Equivra.
Design under review: [approved product design](designs/equivra-payments-workbench.md).
Working artifact destination: this file. Detailed PRD/contracts/task packets will be separate orchestration outputs after the relevant decisions are resolved.
Review depth: implementation-ready, matching the requested project orchestration; technical contracts remain pending until reviewed.

## System audit and recovered decisions

- Baseline HEAD `aaf4eb3`, initial README only; no application, tests, CI, migration tool, or deployed runtime exists. Current untracked `docs/` contains this session's planning artifacts. No stashed work was reported.
- There is no application code to inspect for callers, error handling, test coverage, architectural taste, or runtime reuse. Do not infer safety or implementation from documentation.
- No repository TODO/FIXME/HACK/XXX was found in the original README. No prior refactor/revert or competing feature branch was found in inspected history. Remote PR inventory has not been verified; no claim of its absence.
- Design exists and was approved by the founder's A at D8. Its in-host spec review completed in two rounds with both original findings resolved. It is not a completed CEO/engineering review or an external-model opinion.
- Preserve the product name, payments investigation domain, portfolio-first/business-alongside priority, 10 hours/week, local/synthetic boundary, web workbench, PostgreSQL, one API and one worker process.
- Preserve all nine design success criteria, especially accounting-side evidence, ambiguity, duplicate/replay safety, stale review/freeze conflicts, immutable report snapshots, and reproducibility.
- UI scope is present: import preview, processing state, exception queue, evidence view, review, freeze and export.
- No verified test/build/migration command exists yet. All future paths and commands must be labeled proposed until created and checked.

## Step 0A — premise challenge

The real portfolio outcome is demonstrating financial data correctness and explainable failure/recovery through one usable workflow. A generic payout matcher is a weak proxy for that goal because Stripe already supplies payout reports and open-source engines cover matching. The approved design instead demonstrates evidence gaps, lifecycle events, reviewer concurrency, replay, and snapshot preservation. Doing nothing leaves no runnable portfolio proof; it does not imply an observed customer loss.

## Step 0B — existing leverage

No application code exists in Equivra. Reuse the approved design, synthetic scenario definitions to be authored, native database constraints/transactions, and suitable established libraries after evaluation. Do not rebuild a general ledger, queue framework, or universal financial platform. Framework/library selection and source contracts remain open technical work for the review and orchestration.

## Step 0C — dream-state mapping

```text
CURRENT                     APPROVED FIRST SLICE               POSSIBLE 12-MONTH OUTCOME
README + approved design -> reproducible local investigation -> maintained portfolio evidence;
                            with honest unknowns, reviews,      permissioned customer trials
                            immutable reports and recovery      only if separately justified
```

The right first slice proves the engineering story. It does not promise a commercial launch, paid demand, autonomous accounting, or real payment movement.

## Decision ledger

| ID and owner | Contract and evidence | Current | Proposed | Status | Exact approval and scope |
|---|---|---|---|---|---|
| CEO-BASE — founder | Discovery ledger DISC-01/04/05/06/08/09; approved design | Full first slice and nine acceptance criteria | Retain exact approved behavior in review | approved | D3 A, portfolio-first reply, 10 hours/week, D5 A, D7 B, D8 A |
| CEO-MODE — founder | Mode menu at D9 | HOLD SCOPE | Preserve approved scope and review its correctness/operability | approved | Founder replied "a" to D9; mode alone approves no feature additions or cuts |
| CEO-IMPORT-01 — founder | D10 source-correction choice | Complete three-source bundle per correction revision | Retain original bytes and earlier snapshots; rerun the complete bundle | approved | Founder replied "A" to D10; correction flow and its directly required replay/version regressions |
| CEO-ACCESS-01 — founder | D11 local-access choice | Temporary per-start access code, plus strict loopback/Host/browser boundaries | Reject missing, invalid, and previous-start credentials for application data/actions | approved | Founder replied "A" to D11; no SaaS accounts or hosted access approved |
| CEO-VOLUME-01 — founder | D12 first-demo workload choice | Up to 10,000 data rows and 10 MiB per source; all three sources required | Reject either exceeded limit visibly; record actual measurements | approved | Founder replied "A" to D12; no throughput/latency promise or 100,000-row support |
| CEO-SOURCE-01 — architect / engineering review | Approved three-source financial scenarios, no CSV fixtures/schema exists | Exact fields/signs/dates/source coverage/state mappings not yet frozen | Define authoritative source contracts and scenario expected results before behavior implementation | unresolved | Engineering owner must resolve; not delegated to a builder |
| CEO-RUNTIME-01 — architect / engineering review | Approved API/worker/PostgreSQL shape, no application configuration exists | Runtime/library/API/DB/job/access transport contracts and commands not yet frozen | Lock architecture and foundation verification before consumer task packets | unresolved | Engineering owner must resolve; not delegated to a builder |

No new approach decision is needed before selecting the review mode: D7 B and D8 A settled the current approach. New material implementation or scope choices will be resolved when their review sections establish the evidence.

## D9 — mode selection, A selected

The approved design already bounds the first slice. Exact implementation file ownership/count is not yet established; this is both a new system and an already bounded approved capability, so mode categories overlap. Recommend HOLD SCOPE to scrutinize correctness and feasibility under the 10-hour weekly constraint while preserving the accepted scope. Do not assume a >15-file inventory or silently cut features.

- A: HOLD SCOPE (recommended). Review the complete approved slice; prioritize correctness, failure paths, testing, and operability. Keeps ambition stable but does not provide an expansion scan.
- B: SELECTIVE EXPANSION. Review the baseline and offer additions individually. Could uncover useful improvements but adds decision and sizing work.
- C: SCOPE EXPANSION. Explore the larger product vision and offer additions individually. Broadens the vision but risks distracting from the first demonstrable local release.
- D: SCOPE REDUCTION. Propose a smaller first release, with every cut requiring a separate decision. Can shorten initial delivery but may remove approved portfolio demonstrations if the founder agrees.

The modes differ in kind, not coverage; no completeness score applies. The founder selected A, HOLD SCOPE.

## Step 0G — complexity and minimum complete scope

The application necessarily has a UI, API and worker sharing PostgreSQL. Those boundaries serve the approved interactive workflow and interrupted-job demonstration. Keep one backend codebase and one database; do not introduce independently deployed domain services. Exact future file count remains unknown, so do not invent a file-count justification for cuts. No feature deferrals or additions are proposed. The synthetic-data, USD, local-review boundaries are already approved exclusions, not new cuts.

## Step 0I — temporal interrogation

| Build stage | What must be settled | What surprises an implementer | Required disposition |
|---|---|---|---|
| First foundation work | Supported CSV versions, signs, dates, references, expected synthetic outcomes | Three readable files can still describe different periods or accounts | Document source manifests and unsupported cases before domain implementation |
| First core logic | Economic identity versus file identity; explicit relationships versus candidates | Same amount is not identity; corrected input must not mutate past evidence | Preserve source identities, versioning and unresolved outcomes already approved at D8 |
| Integration | Durable job transaction, replay ownership, current working revision | Process restart or stale worker can publish outdated results | Version-owned processing and guarded publication must prove D8 recovery guarantees |
| Review and export | Expected review/run version and freeze boundary | Review can change while a report freezes | Enforce D8 stale-review/freeze conflict behavior, not last-write-wins |
| Demonstration finish | Clean-machine setup and deterministic fixtures | A successful developer environment is not reproducible distribution | Document and verify actual commands after scaffolding; none exists today |

Prior planning allowance: 90–140 human hours without AI, 60–100 hands-on hours with AI assistance. It is not a measured estimate or a commitment. At 10 hours/week, the latter corresponds to about 6–10 weeks before uncertainty; refine after contracts and first integration. This table is build sequencing, not a claim that those stages fit into a few literal hours.

## Section 1: Architecture Review — reviewed at application-boundary level

### Current scope

HOLD SCOPE selected explicitly at D9 a. CEO-BASE retains D3 A, portfolio-first instruction, 10 hours/week, D5 A, D7 B and D8 A. Accepted: three-source synthetic payments investigation, exact-money evidence, repeat-safe processing, versioned corrections, stale-review protection and immutable reviewed workpapers. Advertising reconciliation was not selected. Hosting, real data, AI, live connectors and SaaS tenancy remain outside the first slice; they are not approved additions. No new scope deferrals are proposed. CEO-IMPORT-01 was resolved by D10 A; later approval history is recorded in its ledger row.

### System and coupling

```text
BEFORE: README + planning documents; no running components

AFTER (approved application shape; detailed interfaces pending):

 Local browser (React)
       | same-origin local requests
 TypeScript API -----------------> source storage (generated IDs, immutable bytes)
       |                                      |
       +---- PostgreSQL <---- TypeScript worker+
             source/run/review   parse, investigate, render
             versions and jobs
```

The API/worker share domain contracts and migrations intentionally; the same application owns them. Never pass arbitrary client filesystem paths to the worker. Store jobs as references to a pinned input revision, not mutable filenames or an unversioned "current" workspace.

### Source upload and processing paths

```text
Happy: selected files -> validate declared source scope -> immutable input revision
      -> durable job -> staged result -> guarded publication -> evidence queue
Nil:  missing required source -> name missing source -> no complete runnable bundle
Empty: zero-byte/unreadable CSV -> validation issue; header-only requires explicit
       supported empty-source semantics, never an implied fully reconciled result
Error: storage/DB/worker failure -> visible failed/retrying job; no partial result
       presented as completed; original bytes retained for diagnosis/replay
```

### Review, freeze and export paths

```text
Happy: pinned case evidence -> expected-version disposition -> draft report
       -> expected-version freeze -> immutable snapshot -> rendered export
Nil:  missing case/run/snapshot -> visible not-found; never select another run
Empty: zero cases -> show source coverage and zero-case result, not proof of
       complete financial records; empty comment is not missing evidence
Error: stale review/freeze -> conflict and reload; render failure -> keep frozen
       snapshot intact and allow regeneration, never silently revise its facts
```

The exact HTTP/status/schema contracts remain to be locked; these paths apply the D8 behaviors rather than inventing an API.

### Conceptual state boundaries

```text
Input: validating -> rejected OR accepted immutable revision
Job:   queued -> running -> completed; transient failure -> retry -> running
                         -> exhausted/invalid -> visibly failed
Run:   processing -> completed OR failed; published results belong to its revision
Case:  unreviewed -> disposition(v+1); stale version -> conflict, no write
Report: draft -> frozen snapshot -> export available OR export failed/retry
        later correction -> NEW draft; frozen snapshot never returns to draft
```

Invalid transitions require DB constraints/conditional writes and transactional publication; a UI-disabled button alone cannot enforce them. The choice of queue and exact transition contract is technical review work, not delegated to a builder.

### Failure, security and scale assessment

- PostgreSQL and local source storage are single points of failure. The demo must fail visibly when either is unavailable, retain immutable inputs, and prove restart/replay. Disaster recovery mechanisms remain for Sections 8–9.
- API-to-worker publication can race with input correction. Pin every job to its immutable revision and prevent a stale job from replacing newer state. D8's correction/replay invariants require this; both completion orders need a controlled integration test.
- Report rendering must read a frozen snapshot, not current mutable cases. This is directly required by D8's reproducibility criterion.
- Local-only does not establish a browser security boundary by itself. Same-origin/host checks, mutation protection, upload/resource limits, and safe escaping remain Section 3 work before implementation. Synthetic-only scope does not excuse arbitrary file access or local cross-site mutations.
- At 10x source volume, parsing, evidence materialization and database indexes are likely first limits; at 100x, resource bounds, query plans and worker backlog dominate. No supported volume or latency claim is established. Section 7 must define a bounded demo envelope rather than claim production scale.
- Rollback must stop API/worker, preserve DB and source bytes, and restore a compatible application/schema pair; actual recovery time must be measured after implementation. Never suggest resetting data as recovery for approved snapshots.

### Architecture decision gate

CEO-IMPORT-01 resolved by D10 A: every correction creates a new complete three-source bundle revision. Older revisions and frozen workpapers remain addressable. Workers and run results are owned by the specific bundle revision; consumers do not discover an implicit mixture of current files. Required tests follow directly from D8 and D10: original frozen output remains unchanged after a corrected bundle, repeat bundle processing produces no duplicates, and stale jobs cannot replace a newer revision's results. Section 1's source-correction gate is resolved. Detailed financial source and runtime contracts are still pending technical design; this application-boundary review does not make them implementation-ready.

## Answered decision (CEO-IMPORT-01)

| Commitment | Authority | Current | A | B |
|---|---|---|---|---|
| Three required source kinds | D8 A | Retain | Retain | Retain |
| Immutable original evidence and frozen reports | D8 A | Retain | Retain | Retain |
| Safe repeated imports and stale jobs | D8 A | Retain | Retain | Retain |
| Correction unit | Unchosen | Pending | New complete bundle revision | Replace one source; create manifest pinning all three source versions |
| Missing source behavior | D8 required evidence | Cannot claim complete supported data | Reject incomplete bundle | New source set cannot run until all required versions are pinned |
| Consumer handoff | Pending implementation contract | Pending | One immutable bundle identity | Immutable manifest plus per-source revision identities |

Question: D10 — How should a reviewer correct imported data?
Project: Equivra/main, approved local synthetic payments workbench.
ELI10: If an accounting CSV is corrected after an investigation, Equivra needs a clear way to start a new version without changing the old report. Requiring a full bundle is simpler; replacing individual files is more convenient but must prevent accidental mixes of old and new evidence.
Stakes: a mixed or silently updated source set can produce a misleading investigation or an irreproducible report.
Recommendation: A because complete bundles give this small local demonstration one clear revision boundary while preserving every approved correctness guarantee.
Note: options differ in interaction and architecture, not coverage; no completeness score.
Header: Correct source data
A) Re-upload the complete bundle (recommended)
Effort S; risk low; reuse the same validation/import path. A correction uploads the three files together as a new immutable revision. It keeps source versions coherent and makes replay tests simpler, but requires reselecting unchanged files. Verify all three sources belong to the new revision, duplicate replays are safe, and past snapshots remain unchanged. Planning allowance for this correction behavior only: human 4–8h / AI-assisted hands-on 3–6h, to be refined.
B) Replace individual source files
Effort M; risk medium; reuse source validators with an additional versioned manifest contract. A reviewer replaces one file while the new revision explicitly pins the other two versions. It avoids unnecessary re-uploads and helps iterative corrections, but adds manifest, stale-job and mixed-version checks. Verify unchanged versions remain pinned, incomplete sets cannot run, and concurrent replacements cannot silently overwrite each other. Planning allowance for this correction behavior only: human 8–16h / AI-assisted hands-on 6–12h, to be refined.
Net: choose a simpler complete-bundle correction flow or more convenient individual replacement with additional version coordination.

Answer: Founder selected A. Apply the complete-bundle correction flow only. The comparison above is retained as question history, not a second open choice.

## Section 2: Error & Rescue Map — Error & Rescue Registry

**WARNING:** no executable error handling or tests exist. The following named operations and error codes are proposed implementation contract names, not symbols found in the repository. They translate the approved D8/D10 outcomes; the orchestration must assign source paths and concrete framework exceptions before any task is ready.

| Proposed operation | Trigger / error class or code | Rescue behavior | User result | Required proof / authority |
|---|---|---|---|---|
| acceptBundle | MissingSource / InvalidManifest / UploadLimitExceeded | Reject as invalid; retain actionable diagnostics; no runnable accepted revision | Which source/field is invalid; no success state | D8 validation/coverage; D10 complete bundle |
| storeSource | SourceWriteFailed / DatabaseUnavailable | Do not acknowledge a runnable bundle before durable bytes and its DB references exist; abandon incomplete staging safely | Upload failed, safe to retry; no partial complete bundle | D8 interruption/replay; inject storage and DB failure separately |
| parseSource | InvalidCsv / InvalidUtf8 / MissingColumn / InvalidValue | Stop invalid import, show bounded source/row/column diagnostics; do not retry malformed content as transient | Correct data and submit a complete new bundle | D8 invalid/missing source behavior |
| normalizeMoney | UnsupportedCurrency / InvalidPrecision / AmountOutOfRange | Reject the invalid value; never coerce/round into a valid financial amount | Source row and reason | D8 exact money/currency; values at boundaries |
| investigateBundle | MissingEvidence / AmbiguousRelation / UnsupportedMovement | These are explicit investigation outcomes, not swallowed exceptions; publish evidence/coverage with unresolved classification | Supported facts plus visible unanswered questions | D8 uncertainty and accounting evidence |
| processRun | WorkerInterrupted / TransientDatabaseFailure | Durable retry/recovery, with result publication guarded by revision and job ownership; finite retry exhaustion is visible | Queued/retrying or failed with action, never a false completed run | D8 interrupted-job and repeat-safe scenarios |
| publishRun | DuplicateResult / StaleJobOwner / ConstraintViolation | Reuse already committed identical result or reject stale publisher; unexpected invariant violation fails loudly | Stable existing result or visible failed job | D8 no duplicate financial outcome; controlled competing publishers |
| saveDisposition | CaseNotFound / StaleCaseVersion / InvalidDisposition | Not-found or conflict without a write; validate input before mutation | Reload current evidence or correct decision | D8 stale review; exactly one write wins |
| freezeWorkpaper | RunNotCompleted / StaleRunOrReviewVersion / MissingSnapshotInput | Reject freeze transaction; do not create a partly frozen report | Not ready or changed since review; refresh | D8 freeze boundary and reproducibility |
| renderWorkpaper | SnapshotNotFound / ExportWriteFailed / InvalidSnapshot | Render only the immutable snapshot; failed rendering never changes snapshot facts; repeat export can retry | Export failed, frozen report retained | D8 report preservation and repeatability |
| readEvidence | RecordNotFound / SourceIntegrityMismatch / ReadFailure | Reject invalid IDs; expose evidence unavailable rather than empty evidence masquerading as valid | Evidence unavailable with correlation reference | D8 traceability; mismatched digest cannot silently pass |

### Error flow

```text
Request/job -> boundary validation -> domain work -> commit/publish
                  |                    |                |
             invalid input       known uncertainty   transient dependency
             named rejection     explicit case       durable bounded retry
                                                        |
                                                exhausted -> visible failure

Unexpected invariant error -> rollback -> fail job/request -> safe redacted diagnostic
Never: catch all -> empty result -> completed/reconciled
```

Rescue is a plan requirement, not verified implementation. Retry intervals, maximum attempts and queue exception mapping remain a technical contract decision; do not publish invented numeric promises. Retry must never re-execute a financial side effect outside a repeat-safe publication boundary. A generic catch may exist only at the process/request boundary to record and return a safe failure; it must not classify unexpected errors as success. Include operation, bundle/run/job IDs, error code and correlation ID in logs; exclude raw rows, file text, startup credentials and account data. AI/refusal/provider failures are N/A because no model call is in the approved slice.

Disposition: the existing approved error/uncertainty/replay/freeze requirements cover this map; no new customer capability or independent verification scope was added. Concrete symbol paths and commands remain unverified until the technical contracts/scaffold exist. Proceed to security review; do not call this tested or implementation-ready.

## Section 3: Security & Threat Model — local-access gate pending

The local-only boundary must be enforced, not merely documented. Primary sources: [MDN Origin](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Origin), [MDN Sec-Fetch-Site](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Sec-Fetch-Site), and [OWASP CSRF prevention](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html). Origin is not guaranteed on all request shapes; CORS alone is not mutation protection. Treat non-browser clients and browser-origin checks as distinct trust questions.

| Threat / boundary | Likelihood | Impact | Required treatment under approved design | Evidence state |
|---|---|---|---|---|
| Malicious website sends requests to local API | Medium | High | Loopback binding, exact allowed Host, same-origin UI/API, reject cross-site mutation requests and disallowed/opaque origins, deny wildcard credentialed CORS | Access mechanism choice below; implementation/test absent |
| DNS rebinding / unexpected Host | Low | High | Reject unconfigured Host; do not trust forwarded headers or a client-provided origin to define the allowed origin | Mandatory local boundary work at D8; test with attacker Host |
| Upload path traversal or arbitrary file read | Medium | High | Server-generated storage identifiers; no client path use; bounded streaming parser; server-owned storage paths; reject unsupported file types | Mandatory source-storage validation at D8; implementation absent |
| Oversized file/field/row count, malformed UTF-8 or CSV | Medium | Medium | Enforce byte/row/field bounds and parser deadlines before resources are exhausted; exact demo limits remain Section 7 decision | D8 safe parser; numeric limits pending |
| Stored HTML/script in filename/note/CSV cell | Medium | High | Render as escaped text; never raw innerHTML or executable report content; self-contained report with inert source text | D8 safe escaping; tests must exercise the user-visible report |
| Spreadsheet formula payload in exported free text | Medium | Medium | Safe spreadsheet export encoding for untrusted text, with original raw bytes retained separately; monetary values come from typed exact values | D8 output safety and raw lineage; exact encoding in export contract |
| SQL/command injection through references or names | Low | High | Parameterized DB access; no shell execution using source text; identifier allowlist/typed ID validation | D8 trust boundary; no implementation yet |
| Guessed or cross-run object IDs | Medium | Medium | Pin every relation to the owning bundle/run; reject cross-revision links and invalid IDs; a local single reviewer is not SaaS tenant isolation | D8 source/run lineage; negative tests required |
| Credentials or financial records in logs | Medium | High | Synthetic fixtures only; redact source text and secrets; rotate any future startup credential per process; no secrets committed | D8 synthetic/local boundary; startup mechanism pending |
| Compromised dependency / unsafe parser defaults | Low | High | Keep dependency count small; inspect license/maintenance and pin lockfile when dependencies are selected | No dependency selected/installed yet |

### Inputs and sensitive writes

All proposed operations below are within one local reviewer boundary. This is a proposed API surface inventory, not an implemented route registry.

| Operation | Input validation / authority | Mutation / visibility |
|---|---|---|
| Upload bundle | Exactly three supported source kinds, allowed currency/account/period, bounded UTF-8 CSVs; ignore client filesystem paths | Creates immutable source revision; no financial writeback |
| Start/retry investigation | Existing accepted bundle ID; job/revision ownership; repeat-safe request | Publishes only the result owned by that revision |
| Read run/case/evidence | Typed identifiers and same owning revision | Read-only; no missing-ID fallback to another run |
| Save disposition | Allowed disposition/text, expected case version, valid evidence references | Append auditable review revision; preserve source facts |
| Freeze report | Completed selected run, expected run/review versions, complete snapshot references | Atomic immutable snapshot; unresolved state remains labeled |
| Download export | Existing frozen snapshot, safe content type/disposition and escaped output | Reads fixed facts; failed export cannot mutate snapshot |

Sensitive mutations require audit events linked to stable local reviewer identity and request/run versions; no need to add multiuser roles. API/worker DB credentials must be local configuration and never committed. Application credentials cannot bypass source validation, version guards or constraints.

### Security decision gate

Historical checkpoint, now resolved by D11 A: require a short-lived startup access code. Both options retain strict browser-origin/Host checks and loopback binding. No public hosting, account system, real data, or SaaS identity is approved by either option. This does not change the financial behavior. Subsequent sections below record the later review work.

## Answered decision (CEO-ACCESS-01)

| Commitment | Authority | Current | A | B |
|---|---|---|---|---|
| Synthetic data and loopback-only service | D8 A | Retain | Retain | Retain |
| Exact allowed Host and browser mutation checks | D8 local boundary; Section 3 threat map | Required enforcement | Retain | Retain |
| Hosted accounts/tenancy | D8 exclusions | Outside slice | Outside slice | Outside slice |
| Access from local clients | Pending | No policy selected | Valid per-start access code required | Trusted local clients may access without a code |
| User interaction | Pending | Unchosen | Enter code shown by local launcher, once per API start | Open local workbench directly |
| Proof | Approved safe-boundary requirement | Pending | Missing/invalid/old code denied; valid code succeeds; origin/Host attacks still fail | Origin/Host attacks fail; document that local clients are trusted |

Question: D11 — Should the local demo require a temporary access code?
Project: Equivra/main, local synthetic payments workbench.
ELI10: A service on your laptop still needs browser protection. We also need to decide whether any local client can open the workbench, or whether it must know a code generated when the API starts.
Stakes: without a code, other local clients are part of the trusted environment; a code adds an access boundary but is not protection against a compromised laptop.
Recommendation: A because a temporary code adds a clear access boundary without building SaaS accounts or a password database.
Note: options differ in trust model and workflow, not coverage; no completeness score.
Header: Local demo access
A) Temporary startup code (recommended)
Effort S; risk low; use standard cryptographic randomness and existing HTTP middleware rather than an account system. Require a per-start code for application data/actions, reject missing/incorrect/previous codes, avoid URLs/logging/persistent storage of the code, and retain same-origin/Host protections. It limits casual access by clients without the code and demonstrates an explicit boundary, but adds a once-per-start entry step and credential handling. Estimated implementation/verification effort: human 3–6h / AI-assisted hands-on 2–4h, provisional.
B) No code; trusted local environment
Effort S; risk medium; retain loopback-only, strict same-origin/Host controls and the same upload/version protections. The UI opens directly and needs no credential storage or entry step. Other local clients may access the synthetic workbench; document and test that boundary, and do not present this configuration as appropriate for hosting or real customer data. Estimated implementation/verification effort: human 2–4h / AI-assisted hands-on 1–3h, provisional.
Net: a small startup access step versus trusting all local clients; both keep public access outside scope.

Answer: Founder selected A. Require a per-start code for application data/actions and invalidate previous-start access, while preserving the fixed loopback/browser controls. No optional second opinion or hosted authentication was authorized by this answer. The table above is retained question history.

## Section 4: Data Flow & Interaction Edge Cases

### Data paths and shadow paths

```text
SOURCE BUNDLE -> VALIDATE -> PARSE/NORMALIZE -> STAGE -> ACCEPT REVISION -> JOB
  missing kind -> reject with source name; no accepted partial bundle
  empty/wrong type/invalid encoding -> source/row diagnostic; no coercion
  too long/too many -> bounded rejection before unbounded buffering
  write/DB failure -> visible failure; no accepted dangling source reference
  duplicate -> stable existing revision/result; no duplicate economic events
  correction -> complete NEW immutable bundle, never an in-place overwrite

JOB -> PINNED INPUT -> DOMAIN CHECKS -> STAGED RESULTS -> GUARDED COMMIT -> CASES
  missing evidence/unsupported movement -> explicit unresolved case
  parser/worker exception -> failed/retrying job; partial results not completed
  lost ownership/duplicate worker -> reject stale publish or reuse committed result
  old revision completes -> retain under its own revision, never replace newer one

CASE + EXPECTED VERSION -> VALIDATE DECISION -> CONDITIONAL SAVE -> AUDIT + RESPONSE
  invalid decision/ref -> reject without mutation
  stale/missing case -> conflict/not-found; require reread of correct evidence
  connection drops -> inspect version/result before repeating, not blind overwrite

RUN + EXPECTED REVIEW SET -> FREEZE TRANSACTION -> IMMUTABLE SNAPSHOT -> EXPORT
  run incomplete/stale reviews -> reject entire freeze
  source/ref integrity failure -> fail visibly, never publish an empty report
  export failure -> retain snapshot; safe repeat rendering
  later changes -> new reviewable version; old snapshot is unaffected
```

### Shared-state invariant and concurrency schedules

The boundary is each committed bundle/run/review/snapshot. No completed API response may claim a state that was not durably committed. No worker may publish into another revision. Freeze must capture the exact review set the reviewer requested, not a mixture across awaits. The schedules below are required regression scenarios, not observed passing tests. `pause/release` means a controlled test barrier; wall-clock sleeps are not proof.

**Duplicate bundle submissions, both commit orders:**

```text
Order 1                 Upload A                Upload B           Shared state
                         stage bytes            stage same bytes   none accepted
                         accept revision R                         R owns source set
                                               accept -> existing R one R
Fresh read: one logical revision and stable result identity

Order 2                 Upload A                Upload B           Shared state
                         stage; pause           accept R           R exists
                         resume -> existing R                     one R
Fresh read: same identity; legitimately equal rows with different source IDs survive
```

Mechanism to lock before implementation: bundle-level replay identity plus DB uniqueness and conflict handling; source-row dedup must not use amount/content alone. A disconnected client reuses its replay identity and sees the committed result. Rerunning with changed source bytes creates a new bundle revision, as D10 requires.

**Worker A loses its lease and worker B retries, both publish orders:**

```text
Order 1                 Worker A               Worker B           Job/result
                         compute; pause         acquire retry      owner B
                         stale publish rejected publish            one committed result
Fresh consumer sees B's committed run, not half-written A data

Order 2                 Worker A               Worker B           Job/result
                         compute; pause         acquire + publish  completed
                         late publish rejected                     same completed result
Fresh consumer sees exactly the same financial result
```

Mechanism: library job ownership plus transaction/conditional publication keyed to job, run and revision; unique published-result ownership. A queue promise of at-least-once delivery does not prove exactly-once effects. Verify a crash before and after commit, not merely before computation.

**Old revision processing versus corrected bundle acceptance:**

```text
Order 1                 Old worker R1          Correction R2       Workspace
                         finish R1              accept R2          R2 selected
Fresh consumer selecting R2 sees only R2's queued/running/completed state

Order 2                 Old worker R1          Correction R2       Workspace
                         paused                 accept R2          R2 selected
                         finish R1                                 remains R2
Fresh consumer may inspect R1 explicitly; R1 cannot replace R2's selection/results
```

Mechanism: immutable revision ownership and guarded workspace selection. A corrected bundle does not require deleting or rewriting a valid old result.

**Two reviewers submit the same expected version:**

```text
Order 1                 Review A               Review B           Case
                         save expected v        pause              v+1 (A)
                                               save v -> conflict v+1 (A)
Order 2                 Review A               Review B           Case
                         pause                  save expected v    v+1 (B)
                         save v -> conflict                        v+1 (B)
Fresh consumer sees exactly one successor and an auditable decision
```

Mechanism: conditional write/transaction over the expected version; never last-write-wins.

**Save disposition overlaps freeze:**

```text
Order 1                 Save decision          Freeze report       Review set
                         commit v+1             freeze expects v    conflict, no snapshot
Fresh consumer refreshes and deliberately freezes v+1

Order 2                 Save decision          Freeze report       Review set
                         pause                  freeze v commits   immutable snapshot v
                         save -> new reviewable version            snapshot v unchanged
Fresh consumer sees the old frozen report and a new draft, not mutated old evidence
```

Mechanism: freeze and review writers coordinate on the same aggregate version/lock in a transaction; snapshot references are immutable. An isolated `SELECT` followed by a later unguarded write is insufficient even if both happen in transactions. Exact locking/isolation contract remains technical design work; approved assertions are fixed.

**Export overlaps later correction, both orders:**

```text
Order 1                 Export snapshot S      Correction R2       Output
                         read/render S          accept R2          facts from S only
Order 2                 Export snapshot S      Correction R2       Output
                         pause                  accept R2          S preserved
                         render S                                  same facts from S
Fresh consumer rendering S sees its original source references and review decisions
```

Mechanism: renderer accepts snapshot identity only; it never joins mutable "latest" review/run pointers to fill report facts.

### Interaction edges

| Interaction | Edge case | Plan handling / authority |
|---|---|---|
| Enter startup code | Wrong code, restart, expired access | D11 A rejection and fresh access step; no hidden mutation retry |
| Upload/start | Double-click, duplicate request, lost response | Stable replay identity and result lookup; D8 no duplicates |
| Preview/processing | Navigate away or refresh | Persisted revision/job status; resume by ID, not in-memory-only progress |
| Correct source | Missing one source, changed period, unchanged replay | D10 complete-bundle validation; create revision only from accepted source set |
| Case list | Zero results or many cases | Coverage summary and bounded paging; zero cases is not completeness proof |
| Evidence | Missing reference, unavailable source, long/unicode text | Explicit unavailable/invalid state; escaped bounded text and preserved raw evidence |
| Save review | Stale tab, competing request | Expected-version conflict; preserve user's draft text while showing current state |
| Freeze | Changed case while request is pending | Aggregate version guard, all-or-nothing snapshot |
| Export | Failed download/render, repeat export | Snapshot remains fixed; regenerate/download safely |
| Retry processing | Failed, duplicate or backlogged job | Visible durable state and bounded retry; stale worker publication rejected |

Disposition: these schedules and assertions directly exercise D8, D10 and D11 commitments. They are mandatory proof for those behaviors, not an optional load/chaos project. No new scope choice is needed in this section. Implementation and passing evidence remain absent.

## Section 5: Code Quality Review

No source methods exist, so method complexity, duplicate implementation and adherence to framework patterns cannot be measured. The risk is creating a large framework before proving one financial story. Keep a single backend codebase with pure money/relationship rules, source-specific parsing, persistence and worker adapters, and a small UI. These are responsibility seams, not a mandate for multiple packages or services.

Required review checks when code exists: do not place financial rules in React or queue callbacks; reuse one validation/error shape per boundary; retain source error context; use names describing evidence and unresolved outcomes rather than claiming "fraud" or "recovered revenue." A catch-all may report an unexpected failure at the outer boundary but may not return an empty successful reconciliation. Do not build a generic plugin system, universal matching DSL, agent/provider abstraction, custom scheduler, or adapter framework for hypothetical sources.

Potential quality findings: (1) API/worker can duplicate validation unless both consume one documented domain contract; (2) raw CSV strings can drift into monetary arithmetic unless normalization creates typed exact values once; (3) mutable UI assumptions can bypass freeze/version contracts unless server enforcement is independent. These are addressed by the approved source/evidence/version guarantees; specific source files will be marked CREATE in orchestration. No speculative refactor is approved. Flag methods with more than five branches during implementation review, but do not invent today's complexity metrics.

Disposition: preserve current application boundaries and existing correctness requirements; no new independent product decision. Runtime/library/file choices remain the architect's responsibility before task handoff.

## Section 6: Test Review

No tests, runners, commands, eval suites or prompt files currently exist. Every item below is a required planned proof, never an executed result. Commands must be established by the foundation task and read back from actual package configuration before consumer packets claim them verified. The plan does not invent `npm test` as an existing command.

### Test flow diagram

```text
Synthetic source scenarios [unit fixture expectations]
              |
parse + money + references [unit: invalid/empty/boundary]
              |
upload / PostgreSQL / job transaction [integration: replay, failure before/after commit]
              |
worker / investigation / publication [integration + contract: interruption, stale owner]
              |
API / UI evidence + review [contract + one E2E journey: not-found, empty, stale save]
              |
freeze + immutable snapshot [integration: concurrent review/freeze both orders]
              |
HTML/CSV report [unit escaping + integration reproducibility + E2E download]

Local access guard [negative integration/browser: missing/old code, cross-site/Host]
```

### Requirement-to-assertion matrix

| Requirement | Observable assertion and wrong result rejected | Layer / owner |
|---|---|---|
| D8 criterion 1, source traceability | Every reported monetary fact resolves to its source rows/calculation; reject orphan citation or invented fee | Unit domain + integration report; financial/report task |
| D8 criterion 2, unknowns | Missing references and same-amount alternatives yield explicit incomplete/ambiguous state; reject first-row auto-match or unsupported supported label | Unit domain + API contract; investigation task |
| D8 criterion 3, repeat/recovery | Duplicate submission and crash/retry produce one committed financial result, both commit orders in Section 4; reject additional allocations/results | Integration PostgreSQL/worker; import/job tasks |
| D8 criterion 4 and D10 A, corrections | All three files pin a new revision; previous frozen report facts and references remain equal; reject mutable replacement or mixed implicit source versions | Integration versioning + report; import/freeze tasks |
| D8 criterion 5, review concurrency | Exactly one update with expected case version succeeds; loser receives conflict with no write | Integration concurrent API calls; review task |
| D8 criterion 6, reproducibility | Rendering stored snapshot after later corrections yields the same financial facts/evidence/decisions; reject lookup of latest case values | Integration export; report task |
| D8 criterion 7, local distribution | Clean documented setup runs seeded demo and checks; reject undocumented state/config dependency | Clean-environment integration + release gate |
| D8 criterion 8, accounting-side evidence | Demonstration includes both processor-bank relation and processor-accounting discrepancy with honest evidence scope | Integration fixture + E2E; domain/UI checkpoint |
| D8 criterion 9, freeze boundary | Save remains draft; freeze fixes selected versions; stale freeze creates no snapshot; reject later mutation of frozen data | Integration controlled scheduling; freeze task |
| D11 A, local code | Missing/incorrect/previous-start code cannot read data or mutate; valid current access succeeds; no token in URL/log/storage | Guard integration + browser negative cases; access task |
| D8 safe parser/escaping | Malformed/oversized/invalid values reject visibly; text payload remains inert in evidence and report, source identity remains available | Unit parser/render + one integration boundary; ingestion/export tasks |
| D8 source ownership | Cross-revision IDs cannot create evidence links or save a disposition in another run | Negative integration; API/domain task |

The test that supports a late-night demonstration is a complete synthetic import-to-reviewed-report journey with stable source references, followed by a repeated import and unchanged result. The hostile test is a pair of stale competing reviewers or a source with identical amounts and different identities. The required fault-injection proof is kill/restart before and after result publication, with controlled barriers and inspection of durable state; not random crashes without assertions.

Use mostly pure domain/parser tests, fewer real-PostgreSQL integration tests, and a small E2E set for the critical UI journey and local access. Avoid live APIs/models, fixed sleeps, uncontrolled randomness and machine-speed assumptions. A schema fixture checks provider/consumer contract shape, but cannot substitute for a real DB concurrency test. Volume benchmarking is a distinct Section 7 choice; no arbitrary 100,000-record throughput or p95 target is already approved. LLM evals are N/A until AI is explicitly added.

Disposition: all mapped assertions derive from accepted D8/D10/D11 behavior and its retained caller contracts. Test method boundaries are recorded; exact tools/commands belong to the technical foundation, not a deferred generic "tests later" ticket. No passing evidence exists today.

## Section 7: Performance Review — supported-volume gate resolved

The design has bounded local input but no numeric supported envelope. This is an unresolved behavior, not measured performance. Reject unbounded uploads instead of hoping streaming alone prevents memory/CPU/DB exhaustion. Do not treat the attachment's unaccepted 100,000-record benchmark as a current promise.

| Area | Assessment / mechanism to specify | Evidence/verification |
|---|---|---|
| N+1 evidence reads | Fetch case/page evidence in bounded sets, not one query per row | Inspect planned query and execution plan after implementation |
| Parser memory | Stream or chunk; enforce per-file/row/field limits before full materialization | Boundary tests at limit and one over; peak memory measurement |
| Domain working set | Index identifiers once per bounded revision; avoid all-pairs candidate search | Adversarial identical-amount dataset; inspect complexity and memory |
| DB indexing | Bundle/revision ownership, source external ID lookup, run+case paging, job status/owner, snapshot references | Establish query shapes first; add only indexes that serve them |
| Caching | No separate cache service; immutable snapshot/revision identities permit repeat reads/results safely | Repeated export cannot reuse mutable current-state data |
| Job payload/runtime | Pass revision IDs, not CSV bodies; finite retries; bound concurrent heavy work | Recover interrupted jobs; measure queue wait and processing duration |
| Pools | One API and one worker share the local DB; pool/concurrency limits must fit the supported envelope | Record actual connection maxima and test start/restart behavior |
| Slowest paths | Parse/normalize, relationship investigation, report rendering likely dominate | Measure each on documented dataset/hardware; no estimated p99 asserted |

### Answered decision (CEO-VOLUME-01)

| Commitment | Authority | Current | A | B |
|---|---|---|---|---|
| Source formats / USD / whole bundle / immutable reports | D8/D10 | Retain | Retain | Retain |
| Valid rows per source file | Not chosen | Bounded but unspecified | Up to 10,000 | Up to 100,000 |
| File byte ceiling | Not chosen | Unspecified | 10 MiB per source | 50 MiB per source |
| Bundle composition | D10 A | Three source files | Three files; each ceiling applies | Three files; each ceiling applies |
| Invalid/excessive data | D8 parser safety | Required visible validation | Reject with explicit limit; no partial accepted bundle | Same |
| Edge/failure correctness | D8 | Retain | All approved cases retained | All approved cases retained |
| Throughput/latency | No approved target | Unmeasured | Record actual results, no promised rate | Record actual results, no promised rate |

Both byte and row ceilings apply; whichever is hit first limits the file. Row counting excludes the header but includes input records before domain deduplication. Exact field-size bounds and parser deadlines are technical safety parameters within the selected envelope. A limit test must not silently drop excess rows or split a financial investigation into unrelated runs.

Question: D12 — What volume should the first local demo support?
Project: Equivra/main, 10 hours/week, local synthetic workbench.
ELI10: We need a clear upload limit so the app can reject oversized files safely. A smaller envelope lets us finish the full investigation story sooner; a larger envelope adds stronger volume evidence but needs more tuning and measurement.
Stakes: unbounded inputs can stall the laptop or produce partial results; promising unmeasured speed would undermine the portfolio.
Recommendation: A because 10,000 rows per file already exercises real database and worker behavior while keeping the first finish line achievable.
Note: options differ in supported workload, not correctness coverage; no completeness score.
Header: First demo volume
A) 10,000 rows per file (recommended)
Effort S; risk low; reuse bounded streaming and indexed identifier lookups. Support up to 10,000 data rows and 10 MiB in each of the three source files, rejecting either limit visibly. This provides enough data to exercise jobs/paging and bounds tuning work, but does not demonstrate 100,000-row input support. Added envelope measurement/tuning allowance: human 4–8h / AI-assisted 3–6h, provisional; not a total project estimate.
B) 100,000 rows per file
Effort M; risk medium; retain the same financial contracts and use bounded processing with measured query/memory tuning. Support up to 100,000 rows and 50 MiB per source, with the same validation/replay/report guarantees. It provides a stronger large-input demonstration and reveals scaling pressure earlier, but increases implementation and measurement work; it does not promise a particular speed. Added envelope measurement/tuning allowance: human 10–20h / AI-assisted 6–12h, provisional; not a total project estimate.
Net: a smaller complete first demo versus more scale evidence and tuning work; no accepted financial edge case is removed by either choice.

Answer: Founder selected A at D12. Enforce both 10,000 data rows and 10 MiB per file, with exactly the supported three source kinds. Do not accept a truncated file as a complete source. Measure rather than claim performance. Retain all D8/D10/D11 correctness, uncertainty, replay, review and access assertions. Section 7 disposition: resolved at the supported-workload level; exact parser/query/pool configuration belongs to the engineering contracts.

## Section 8: Observability & Debuggability Review

**WARNING:** no runtime instrumentation exists. The approved visible failure and recovery workflow needs structured diagnostics, not a separate monitoring platform. Treat these as implementation obligations of the existing operations, with the domain/job task owning its own instrumentation and tests.

| Boundary | Working signal | Failure signal | Diagnostic and runbook action |
|---|---|---|---|
| Local API/access | Request completes with correlation ID and operation | Auth/origin rejection count, unexpected failure | Return safe error; never record supplied code or auth header; restart access requires fresh code |
| Upload/validation | Accepted revision, source count, aggregate row counts | Invalid source/limit rejection or incomplete staging | Name the source/field issue to reviewer; remove only unreferenced abandoned staging after safety checks |
| Jobs | Queued/running/completed state and elapsed stage duration | Failed/exhausted job, retry attempt, stale ownership rejection | Inspect durable state by run/job ID; correct malformed data with new whole bundle; retry only eligible job |
| Investigation | Supported/ambiguous/incomplete counts with rule version | Invariant failure or unsupported movement | Show unresolved reason, never convert unknown into success; reproduce from pinned fixture/source revision |
| Review/freeze | Saved revision and snapshot ID with review-set version | Stale write/freeze conflict | Reload current evidence; retain unsaved note; do not auto-approve changed facts |
| Export | Snapshot ID and artifact generation outcome | Render/storage/integrity failure | Keep snapshot, regenerate export safely, verify source integrity before claiming repeatability |

Log operation, outcome, correlation ID, bundle/run/job/snapshot ID, retry number and duration. Do not log raw CSV rows, notes, account/customer names, startup code or DB credentials. IDs must be locally generated references, not embedded personal identifiers. Link job lineage back to its originating request. Entry/exit events and errors must permit diagnosis without dumping every row.

Day-one dashboard means the existing local run/job status UI and a reproducible diagnostic command/report defined in the eventual runbook, not Grafana, a metrics cluster, email/SMS alerts or an admin product. A failed or stalled job must remain visible in that UI; retry exhaustion must never look like continued healthy progress. Any future external alerting is outside this local release. Exact stall thresholds follow the selected queue's job timeout contract, not an arbitrary clock in the frontend.

Verification: induce accepted upload, malformed input, DB outage, worker interruption, stale review and failed export; inspect sanitized correlated events alongside the durable/UI states. These checks prove the already approved visibility/recovery requirements. The eventual integration gate must verify no source text or access secret appears in captured logs. No new telemetry vendor or paid dependency is required.

Disposition: one evidenced gap, absent instrumentation, assigned to behavior-owning tasks. No separate service or optional feature is added. Runbook and diagnostics must be implemented and exercised before claiming operability.

## Section 9: Deployment & Rollout Review

This release is a local synthetic demonstration. There is no hosted environment, staging URL, public deployment, managed database, live connector, or real-data migration. Those checks are N/A for this release, not passed. There is no existing deployment pipeline to reuse.

```text
FRESH LOCAL SETUP
check runtime prerequisites -> validate local config -> start isolated PostgreSQL
 -> apply recorded migrations -> verify synthetic fixture version
 -> start API (fresh access code) + worker -> UI access
 -> import/review/freeze/export smoke -> record observed result

UPGRADE LOCAL SETUP
stop API and worker -> preserve DB + source storage together
 -> apply compatible migration -> start matching API + worker version
 -> verify pending/completed/frozen historical state -> resume demo
```

Migrations are not designed yet. The first database schema is new, but later migrations must preserve previously approved snapshots. Do not run old and new API/worker contracts together accidentally; record a schema/application compatibility version and fail startup loudly on mismatch. Local downtime for coordinated upgrade is acceptable to the first-demo shape; this is not a zero-downtime SaaS claim. No feature-flag platform is needed; the release boundary itself excludes optional AI, hosting, live connectors and real data.

```text
Regression/invariant failure after upgrade?
                 |
            stop API + worker
                 |
    preserve failed state for diagnosis (no reset)
                 |
     restore matching prior DB + source archive
                 |
     start compatible prior API/worker version
                 |
 replay synthetic smoke + prior snapshot reproduction
                 |
    resume only after checks pass; otherwise remain stopped
```

Rollback trigger: source facts change unexpectedly, duplicate outcomes appear, frozen report reproduction fails, or access/ownership enforcement is bypassed. Owner: implementing maintainer/founder. Restore duration must be measured after the runbook exists; no invented time-to-recovery promise. A backup without the corresponding source bytes cannot prove recovery. Snapshot checks compare financial facts and references; artifact metadata may differ only where documented and irrelevant to those facts.

First-five-minute smoke: confirm loopback-only access, missing/old code denial, current access, all three synthetic sources, one visible validation failure, a completed run with explicit unknowns, reviewed snapshot and export. First-hour diagnostic rehearsal: repeat import, interruption around commit, stale review/freeze and restore/reproduction. These are local acceptance checks, not deployed production observation. Reset is only for a clearly designated disposable fixture database and never replaces recovery of a history-bearing dataset.

Disposition: migration/restore and clean-setup evidence absent; assigned to integration/release preparation. Proposed local Compose/config files will be marked CREATE in the orchestration, never described as already present. No rollout scope addition.

## Section 10: Long-Term Trajectory Review

Reversibility: **4/5 at the product architecture level**. UI, process composition and libraries can change while the documented domain contracts survive. Immutable source/report lineage is intentionally durable; changing its meaning requires versioned contracts and migration/recovery proof, not rewriting old facts.

| Debt or path dependency | Why it exists | Upgrade trigger / prevention |
|---|---|---|
| Three fixed CSV formats, USD, synthetic-only | Explicit first-demo boundary, not universal finance support | A separately approved real workflow needs new adapters/contracts and data handling review |
| Local reviewer + startup code | D11 boundary avoids SaaS identity work | Any hosted/shared or real-customer-data plan needs a new auth/threat model before exposure |
| Complete-bundle corrections | D10 gives one clear revision boundary | Revisit only if repeated real usage shows material re-upload burden; preserve history |
| One backend, one worker, PostgreSQL | Approved low-process-count application | Add infrastructure only with measured bottleneck/operational evidence, not portfolio ornament |
| Source/run/report version contracts | Reproducibility and recovery | Document migrations, ownership and fixture expectations so one engineer is not the only source of truth |

This repository has no framework convention yet, so ecosystem alignment cannot be claimed. Prefer one conventional TypeScript setup and a lockfile after technical selection. Knowledge transfer requires source contracts, scenario expected results, state diagrams, runbook and task handoffs. A new engineer should be able to reproduce the demo without a private chat transcript.

No future feature/market expansion is proposed in HOLD SCOPE. The 12-month test is whether the same facts, limitations and recovery demonstrations remain understandable, not whether a larger SaaS was built. A portfolio writeup must label synthetic datasets and measured hardware/results and must not imply production payment movement, customer savings or validated accounting advice.

Disposition: accepted scope remains intact. The debt listed is an explicit boundary, not a hidden waived guarantee or a new TODO proposal.

## Section 11: Design & UX Review

The approved rough workflow sketch exists at `docs/designs/assets/equivra-workflow-sketch.html` and `.png`. No polished DESIGN.md or implemented design system exists. The sketch demonstrates information hierarchy; it is not a visual QA pass.

Lead with the source bundle, then the exceptions and their evidence, then review and report. Avoid a generic KPI dashboard that suggests certainty or savings not established by the sources. Use separate labels for supported evidence, incomplete coverage, ambiguity and reviewer disposition; a frozen report can contain unresolved cases and must say so.

```text
Local access prompt --invalid code--> actionable retry
      |
      v
Bundle upload/preview --invalid/missing/oversize--> source diagnostics
      | corrected complete bundle
      v
Processing status --retry/fail--> visible cause + eligible retry
      |
      v
Exception list --zero cases--> source coverage, no completeness claim
      |
      v
Evidence + review --stale submit--> current version + retained draft note
      |
      v
Draft workpaper --stale freeze--> refresh required, no snapshot
      |
      v
Frozen snapshot (unresolved labels preserved) --export fail--> retry export
      |
      v
Download unchanged reviewed facts

Correction from any completed flow -> NEW complete bundle -> new version,
never overwrite an earlier frozen snapshot
```

| Feature | Loading | Empty | Error | Success | Partial |
|---|---|---|---|---|---|
| Access | Submitting code | Code entry | Invalid/previous code; reconnect after restart | Workbench available | No application data revealed before access |
| Upload/preview | Parsing/validating | Show three required source slots | File/row/field issue and limit | Accepted pinned bundle | Incomplete selection does not become runnable |
| Processing | Queued/running/retrying | No accepted bundle | Durable failed job + reason | Published result for selected revision | No partial result labeled complete |
| Case queue | Fetching bounded page | No cases plus coverage | Request failure with retry | Cases and evidence state | Incomplete/ambiguous cases remain distinct |
| Evidence/review | Fetch/save progress | Missing evidence explicitly named | Conflict/not-found/invalid input | Saved review version | Unsaved draft preserved on conflict |
| Freeze/export | Freeze/render progress | Draft not yet frozen | Stale freeze or export failure | Snapshot/export identity visible | Frozen unresolved cases remain labeled |

Accessibility: implement semantic forms/tables/buttons, explicit labels and errors, keyboard navigation, visible focus, live status announcements, non-color-only evidence states, text/contrast/touch targets suitable for the interface. Move focus to invalid fields or a useful error summary and retain user's source selection/note where safe. Do not hide evidence in hover-only UI. Long identifiers/text must wrap or have a labeled horizontal scroll region rather than clipping facts.

Responsive intention: desktop-first evidence review; narrow screens stack source/evidence and decision panels, keep the original amount/currency/reference readable, allow bounded table scrolling and preserve keyboard access. This is no new mobile application or design-system project. Emotional journey: understand the source scope, trust supported facts, see honest uncertainty, make a deliberate review, obtain a stable artifact.

Disposition: no independent UX feature additions. Full visual design review can follow the detailed plan; after implementation use a rendered design review to verify the actual states, accessibility and responsive behavior. This section does not claim those checks passed on application UI.

## Closing review state

Sections 1–11 have been evaluated in order against the accepted slice. Product decisions CEO-IMPORT-01, CEO-ACCESS-01 and CEO-VOLUME-01 are approved by D10 A, D11 A and D12 A respectively. No scope expansion, new deferral or optional TODO was introduced. Method/file/command contracts remain technical work for the requested engineering/orchestration phase; they cannot be handed to a builder as verified implementation instructions yet. Independent outside review and final report still pending.

## Outside Voice Outcome

Attempt: Claude Code, host Codex, phase CEO plan review. The configured external process exited 1: `API Error: Can't reach the API server — check your internet or DNS (ENOTFOUND)`. It produced no reviewer response or findings. Provider model identity is not established; `modelUsage` was empty. No cross-model agreement or clean-review credit applies.

The required bounded fallback needs a declared Plan subagent type plus TaskOutput and TaskStop tools. Those capabilities are not declared on this host. Per the workflow's unavailable path, no replacement general-purpose reviewer was launched. The prior office-hours spec review remains its own completed in-host review, not a fallback or an outside CEO review.

Saved sanitized attempt metadata: [outside review evidence](reviews/ceo-outside-review.json). The prompt contained the first 30KB of the working plan with an explicit truncation notice and later-section context; the provider received no successful inference response. The private prompt was removed after termination. No retry or provider substitution was made.

Outside voice unavailable. Continuing to planning decisions and Approval readiness. No outside findings exist to integrate. This is missing coverage, not zero findings from a completed review.

## Remaining TODO Choices

None. No unanswered proposal to add a feature, remove approved work, or create a new backlog item was introduced. Unapproved future AI/hosting/connectors/real-data work stays outside the first slice without creating implementation tickets or silently choosing a later delivery date.

## Approval Readiness

Approval readiness: PASS for applied product scope and remedies. Checked CEO-BASE against D3 A, the explicit portfolio-first instruction, 10 hours/week, D5 A, D7 B and D8 A; CEO-MODE against D9 a; CEO-IMPORT-01 against D10 A; CEO-ACCESS-01 against D11 A; CEO-VOLUME-01 against D12 A. The plan applies only those accepted choices and their required correctness/verification obligations.

CEO-SOURCE-01 and CEO-RUNTIME-01 remain explicitly unresolved architect-owned prerequisites; they are not smuggled into approved implementation tasks as settled contracts. There are no unanswered founder product questions at this checkpoint. A navigation choice does not resolve these technical prerequisites or authorize coding.

## NOT in Scope

- Not selected: advertising billing reconciliation (D3 A selected payments investigation), and the CLI-only delivery approach (D7 B selected the workbench).
- Outside the approved first release: real data, hosting, live integrations, AI/model calls, SaaS accounts/tenancy, multiple currencies, payment movement, accounting writeback and universal parsing (D8 A).
- Not selected: individual-file replacement (D10 A), access without startup code (D11 A), and 100,000-row/source support (D12 A).
- Optional discovery second opinion was skipped at D6 b. This did not disable the separate CEO outside review; its actual unavailable result is recorded above.

These are retained exclusions or rejected alternatives, not newly approved TODO deferrals. No TODOS.md update is claimed.

## What Already Exists

Existing: root README, approved product design and static sketch, repository context, decision ledger, [PRD](PRD.md), and [synthetic scenario narratives](demo-scenarios.md). These planning artifacts can be reused directly. Scenario narratives are not executable CSV fixtures. The in-host office-hours review evidence exists in `docs/designs/equivra-review/` and applies to its recorded document version.

Absent: application code, runtime manifest/lockfile, schema/migrations, test harness, CI, runbook implementation and verified application commands. Every code path proposed in the review is a planned operation, not an existing function.

## Dream State Delta

This review takes the project from two conflicting product ideas to a bounded, approved payments investigation demonstration and explicit verification obligations. It does not take it to a running application, proven business, or ready-to-delegate build. The next engineering phase must replace technical unknowns with frozen source/runtime contracts and verified foundations.

## Failure Modes Registry

`Planned` means specified behavior, not implemented or verified. No application test has run. This registry records 13 mechanism groups and zero known silent-success design gaps after the approved remedies; two technical-contract prerequisites remain open.

| Codepath / mechanism | Failure mode | Rescued? | Test? | User sees? | Logged? |
|---|---|---|---|---|---|
| acceptBundle | Missing source / invalid source scope | Planned reject | Required, absent | Named validation issue | Planned code/IDs only |
| storeSource | Disk/DB failure before acceptance | Planned rollback/staging isolation | Required, absent | Failed upload, safe retry | Planned correlated failure |
| parse/normalize | Malformed CSV/value/currency | Planned reject, no coercion | Required, absent | Source/row issue | Planned redacted diagnostic |
| investigate | Missing/ambiguous evidence | Planned explicit unresolved result | Required, absent | Coverage/reason/evidence | Planned state counts |
| processRun | Crash before/after commit | Planned durable recovery | Required, absent | Retrying or failed | Planned job lineage |
| publishRun | Duplicate/stale worker | Planned guarded publication | Required, absent | Stable owning revision | Planned stale rejection |
| saveDisposition | Stale competing update | Planned conflict, no overwrite | Required, absent | Refresh/current version | Planned audit event |
| freezeWorkpaper | Review changes during freeze | Planned atomic version guard | Required, absent | Conflict, no partial snapshot | Planned audit event |
| renderWorkpaper | Export/storage/read failure | Planned preserve snapshot/retry | Required, absent | Export unavailable/retry | Planned snapshot ID |
| access guard | Missing/invalid/old access | Planned deny | Required, absent | Local access prompt/error | Planned no secrets |
| upload/resource guard | Row/byte limit exceeded | Planned reject, no truncation | Required, absent | Exact exceeded limit | Planned bounded diagnostic |
| ownership boundary | Cross-revision IDs/paths | Planned reject | Required, absent | Invalid/not found | Planned boundary rejection |
| output boundary | HTML/formula payload | Planned inert safe rendering | Required, absent | Text, not execution | Planned no raw payload |

The complete operation/error/rescue mapping is the Section 2 Error & Rescue Registry (11 operation groups). No `RESCUED=N, TEST=N, USER SEES=Silent` remedy is accepted. That design result does not mean implemented security/reliability exists.

## Diagram and Stale Diagram Audit

This plan contains system architecture, source/review data flows with shadow paths, conceptual state boundaries, error flow, six paired concurrency schedules, test flow, local deployment sequence, rollback flow and UX state flow. All are proposed designs, not execution traces.

The approved design's system/flow diagrams remain valid with D10 whole-bundle revisions and the later access/resource decisions. The static sketch omits the added access prompt and numeric upload limits; it remains intentionally rough and is not evidence of completed UI coverage. The PRD and this review supersede it for those controls. No existing application diagram was found to become stale.

## Implementation Tasks

These are prerequisite engineering actions synthesized from the review, not builder-ready behavior packets. They precede the requested full orchestration. Known documentation paths below exist; future source paths are **to be determined** by the architect and must be marked CREATE when assigned. No new code is authorized by this review.

- [ ] **T1 (P1, human ~8–12h / AI-assisted ~3–5h)** — Source contracts — Freeze the three adapter schemas, signs, date meanings, identity, evidence scope and scenario expectations.
  - Surfaced by: Sections 1/2/4/6; CEO-SOURCE-01 is unresolved.
  - Files: `docs/PRD.md`, `docs/demo-scenarios.md`, `docs/repo_context.md`; new contract/fixture paths to be determined.
  - Verify: each S1–S8 scenario maps to explicit valid/invalid source fields and observable expected facts; no ambiguity is assigned to a builder; no real-customer or universal-format claim.
- [ ] **T2 (P1, human ~6–10h / AI-assisted ~2–4h)** — Runtime contracts — Lock API/worker/DB/job/access transport/storage choices, failure/retry semantics, immutable snapshots and concurrency enforcement.
  - Surfaced by: Sections 1–5 and 7–9; CEO-RUNTIME-01 is unresolved.
  - Files: `docs/PRD.md`, `docs/repo_context.md`, this review; new ADR/schema/API/runtime paths to be determined.
  - Verify: all Section 4 schedules have enforceable transaction/ownership mechanisms; D11 access and D12 bounds are explicit; no fake existing command or unverified library capability.
- [ ] **T3 (P1, human ~6–10h / AI-assisted ~2–4h)** — Orchestration — Create the contract registry, DAG, file ownership, self-contained packets, fixtures, integration checkpoints and release gate after T1/T2.
  - Surfaced by: Sections 5/6/9/10; architecture is not yet safe to delegate.
  - Files: `docs/repo_context.md`, `docs/PRD.md`, existing approved design/review; new plan/task paths to be determined.
  - Verify: every provider/consumer has explicit compatible inputs/outputs/errors and a fixture; graph acyclic; no same-wave write collisions; required commands explicitly unverified until foundation creation and successful checks; no ready status before required gates pass.

These estimates are planning allowances for review/design work, using roughly 2–3x research/design compression; they are not guaranteed AI speedups or added commitments to a six-week deadline. No separate new implementation task was created for zero-finding scope disposition in Section 10, nor for speculative features. Behavior tests and diagnostics must remain with their owning future packets.

Global `/autoplan` task JSONL aggregation is **not persisted**: its specified destination is outside permitted workspace writes, and no substitute global aggregation path is claimed. The complete task content is saved above in the workspace plan. History/analytics metadata likewise remains unpersisted; this does not unsave these documents.

## Completion Summary

| Item | Actual result |
|---|---|
| Mode / system audit | HOLD SCOPE; baseline README-only, current artifacts are planning/docs |
| Step 0 | Existing product decisions retained; three later implementation-policy choices approved at D10–D12 |
| Section 1 Architecture | Revision/correction gate resolved; source/runtime contracts remain engineering prerequisites |
| Section 2 Errors | 11 operation/error groups mapped; no accepted silent-success rescue gap; implementation absent |
| Section 3 Security | 10 threat groups; 7 High-impact scenarios, not observed vulnerabilities; D11 access decision resolved |
| Section 4 Data/UX | 10 interaction groups and 6 paired concurrency schedules; mechanisms/tests still require implementation |
| Section 5 Quality | 3 implementation risks recorded; no code complexity metrics invented |
| Section 6 Tests | Diagram + 12 requirement/assertion rows; no runnable tests or verified application commands yet |
| Section 7 Performance | 8 areas evaluated; D12 supports 10,000 data rows and 10 MiB/source; no measured performance |
| Section 8 Observability | Instrumentation/runbook evidence absent; behavior-owner obligations recorded |
| Section 9 Deployment | Local setup/upgrade/restore risks recorded; hosted acceptance N/A, not passed |
| Section 10 Future | Reversibility 4/5; 5 explicit boundary/path-dependency rows |
| Section 11 UX | State map + flow; semantic/accessibility/narrow-screen checks specified, not tested |
| NOT in scope / existing / dream delta | Saved above; no new scope cuts or expansion |
| Error/failure registries | 11 operation groups / 13 failure groups; planned controls only, no acceptance evidence |
| TODOs / scope proposals | 0 new TODOs; 0 expansions; no silent deferrals |
| Separate CEO archive | Skipped by HOLD SCOPE mode |
| Outside voice | Claude Code API DNS failure; no completed external review; no declared bounded native fallback |
| Lake score | N/A — all choices differed in kind/workload, none offered scored coverage |
| Diagrams | 9 types: system, data, state, error, concurrency, tests, deploy, rollback, UX |
| Stale diagrams | Rough sketch lacks later access/limit refinements; documented above, not a finished UI claim |
| Unresolved decisions | 2 architect-owned prerequisites: CEO-SOURCE-01 and CEO-RUNTIME-01 |
| Status | DONE_WITH_CONCERNS for CEO review; not ready for implementation/delegation |

No durable memory/skill update was made. The review exposed no additional generalized operational learning requiring a user-approved memory change. No global analytics/history write is claimed. The actual report below is persisted only in this workspace file.

## GSTACK REVIEW REPORT

| Review | Trigger | Why | Runs | Status | Findings |
|--------|---------|-----|------|--------|----------|
| CEO Review | `/plan-ceo-review` | Scope & strategy | 1 | ISSUES OPEN; global history not persisted | HOLD SCOPE; retained approved scope, 2 unresolved engineering prerequisites |
| Outside Review | Claude Code CLI, CEO phase, host Codex | Independent second opinion | 1 attempt | UNAVAILABLE | API unreachable (ENOTFOUND); no completed external review or findings |
| Eng Review | `/plan-eng-review` | Architecture & tests (required) | 0 | NOT RUN | Exact financial/runtime contracts and foundation verification still required |
| Design Review | `/plan-design-review` | Detailed UI/UX review | 0 | NOT RUN | Approved rough sketch exists; no full application design review |
| DX Review | `/plan-devex-review` | Developer setup | 0 | NOT RUN | No executable application setup exists |

**OUTSIDE COVERAGE:** Claude Code, CEO-plan-review phase, unavailable; inference produced no response. The host's required bounded native fallback is undeclared. The earlier in-host office-hours spec review is separate and is not external CEO coverage.

**VERDICT:** CEO scope review recorded with concerns; eng review required. No implementation or delegation clearance. Workspace report saved; global history/aggregation not persisted.

**UNRESOLVED DECISIONS:**
- CEO-SOURCE-01 — architect must freeze supported source fields, monetary signs, timing/lifecycle semantics, evidence scope and machine-checkable scenario outcomes before financial implementation.
- CEO-RUNTIME-01 — architect must freeze concrete runtime/API/DB/job/access contracts and establish actual foundation verification before implementation packets can be called ready.
