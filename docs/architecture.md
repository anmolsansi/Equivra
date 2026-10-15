# Architecture Plan: Equivra

Status: architect-authored v1 design, subject to contract/conformance gates; no implementation or passing runtime evidence.
Authority: approved PRD/design, HOLD SCOPE, D10 complete-bundle corrections, D11 startup code, D12 input envelope, D14 original application arrangement. No product feature additions.

## 1. Stack Decisions

| Layer | Selected technical design | Reason and limit |
|---|---|---|
| Runtime | Node.js 24 LTS baseline, TypeScript compiled ESM | Maintained runtime; typecheck/build before execution. Host currently has Node 25.8.1, not the selected baseline; T01 must pin/prove baseline |
| API | Fastify with its JSON Schema validation; multipart/static plugins | One API with native schema validation and bounded uploads; no controller/service/repository framework |
| Web | React + Vite, native fetch and semantic HTML/CSS | Small interactive review UI; no SSR, router/state/form framework required for five local views |
| DB | PostgreSQL 18; node-postgres parameterized SQL; numbered SQL migrations | Explicit constraints/transactions without ORM indirection |
| Jobs | pg-boss 12.38.0 design baseline; one worker, local concurrency 1 | Existing PostgreSQL-backed queue; no custom scheduler, Redis or broker |
| Sources | csv-parse streaming, immutable files under a server-owned directory | Bounded RFC4180-style parsing; preserve original bytes and fields |
| Auth | Per-API-start 32 random bytes encoded base64url; Bearer header | Browser keeps code only in memory; reload/new tab requires entry again; restart invalidates previous code |
| Tests | Node built-in test runner for unit/integration; Playwright library driven by Node tests for browser journeys | One test runner; browser library is for real interactions, not a second runner |
| Delivery | Local Docker Compose PostgreSQL plus API/worker using a shared Node24 application image | Local-only; one API origin serves built web assets; no cloud deployment |
| AI/cache | None | No model calls or additional cache in approved release |

All dependency versions except the researched pg-boss baseline must be pinned together by T01 in the lockfile after compatibility review. This is a version-resolution obligation, not permission to change framework or architecture. If documented APIs differ, stop that contract and return to architect; do not silently substitute a queue or transaction model.

Primary documentation inspected: [Node releases](https://nodejs.org/en/about/previous-releases), [Fastify validation](https://fastify.dev/docs/latest/Reference/Validation-and-Serialization/), [PostgreSQL row locks](https://www.postgresql.org/docs/current/explicit-locking.html), [pg-boss adapters](https://pgboss.io/api/adapters) and [transactional workers](https://pgboss.io/api/workers). Documentation claims are design evidence, not a successful local compatibility probe.

## 2. Frontend Architecture

**CREATE** `web/src/App.tsx`, `web/src/api.ts`, `web/src/styles.css`; `web/index.html` and Vite/TS configuration are foundation-owned. App state is local React state: access, selected bundle/run, selected case, draft note and selected snapshot. Server objects remain authoritative. Use explicit reload/refetch after conflicts; do not auto-resubmit a changed review or freeze.

API helper attaches in-memory Bearer code, returns typed success/error values, and clears access on 401. Never put code in URL, localStorage, sessionStorage, cookies or an exported artifact. It may be intentionally displayed once in the launcher's interactive terminal, but not in structured application logs or saved diagnostics. UI assets contain no secret. Do not claim this protects a compromised OS/browser extension.

One origin: `http://127.0.0.1:4310`, API serves built web assets. No separate cross-origin development UI is required. User-facing paths can be state-selected within `/`; the API paths below are explicit. Every view covers loading/empty/error/success/partial, keyboard/focus, readable long identifiers and narrow-screen stacking. Preserve draft note on conflict. Frozen report labels unknowns independently from review disposition.

## 3. Backend Architecture

**CREATE** `server/main.ts`, `server/app.ts`, `server/config.ts`, `server/db.ts`, `server/access.ts`, `server/imports.ts`, `server/jobs.ts`, `server/worker.ts`, `server/reviews.ts`, `server/reports.ts`; **CREATE** `shared/source.ts`, `shared/money.ts`, `shared/investigate.ts`, `shared/report.ts`.

`app.ts` creates Fastify and mounts modules; `main.ts` owns startup/shutdown and the fixed local binding profile described in section 8. Modules export route plugins or functions; do not introduce base classes or wrappers around every SQL query. Shared pure functions know nothing about HTTP, queue or filesystem. API and worker consume the same input/rule types. Pino/Fastify structured logging uses redaction and generated correlation IDs, never raw source content or Authorization.

### Entry flow

```text
API: config -> DB/schema compatibility -> current access code -> routes -> fixed local binding (host loopback; container port published on host loopback)
Upload -> access/Origin/Host -> bounded files+manifest -> parse+validate -> immutable paths
       -> transaction(bundle+files+rows+run+queue job) -> 202 pinned identities
Worker -> owned durable job -> pinned normalized records -> pure investigation
       -> atomic result+cases+job completion -> completed run
Review -> lock run -> expected case version -> decision+aggregate version -> commit
Freeze -> lock same run -> expected aggregate version -> immutable snapshot -> commit
Export -> snapshot only -> escaped HTML/CSV, deterministic factual content
```

Failure before upload commit must leave no accepted dangling revision; unreferenced files are staging, never treated as accepted evidence. After files are finalized, a failed DB transaction may leave an orphan, not an acknowledged bundle. Cleanup removes only positively unreferenced staging after a stopped process/verified DB lookup; never delete a referenced file on a failed response.

## 4. Database Architecture

**CREATE** `db/001_initial.sql` and `db/migrate.ts`. Use `equivra` application schema and pg-boss-owned queue schema. No process edits pg-boss internal tables. Application migration version and expected queue version are checked at startup; migrations run as a separate coordinated step, not silently on every API start. Back up DB and source directory together before upgrades.

All identifiers are server-generated UUIDs except synthetic external IDs. JSONB financial amounts are signed integer-minor-unit strings; never JSON floating-point dollars. Immutable objects have `created_at timestamptz`; chronology is not identity. SQL names snake_case; TypeScript/wire names snake_case at boundaries to avoid conversion wrappers.

| Table | Columns and constraints |
|---|---|
| schema_version | `version integer primary key`, `applied_at timestamptz not null`; ordered migrations |
| bundle | `id uuid pk`, `content_key text unique not null`, `manifest jsonb not null`, `created_at`; content_key covers profile/rules-independent canonical manifest + source kind/hash pairs, not filename |
| source_file | `id uuid pk`, `bundle_id fk bundle`, `kind text check in stripe,bank,books`, `sha256 text`, `storage_key text unique`, `bytes bigint check 0<bytes<=10485760`, `row_count integer check 0<=row_count<=10000`; unique(bundle_id,kind) |
| source_row | `id uuid pk`, `source_file_id fk`, `row_no integer check >0`, `raw_fields jsonb`, `normalized jsonb`; unique(source_file_id,row_no); rows immutable |
| run | `id uuid pk`, `bundle_id fk`, `rule_version text`, `job_id uuid unique`, `state text check queued,running,completed,failed`, `review_version integer default 0 check >=0`, `error_code text nullable`, `result jsonb nullable`; unique(bundle_id,rule_version); completed requires nonnull result; incomplete/ambiguous are result evidence states, not worker failure |
| case_record | `id uuid pk`, `run_id fk`, `case_key text`, `kind text`, `evidence_state text check supported,difference,incomplete,ambiguous,unsupported`, `facts jsonb`, `evidence jsonb`; unique(run_id,case_key); evidence references must resolve within the run's bundle in validated publication transaction |
| decision | `id uuid pk`, `case_id fk`, `version integer >0`, `disposition text check noted,needs_evidence`, `note text <=2000 code points`, `created_at`; unique(case_id,version); append-only; current case version is max decision version or 0 |
| snapshot | `id uuid pk`, `run_id fk`, `review_version integer`, `payload jsonb`, `payload_sha256 text`, `created_at`; unique(run_id,review_version); immutable; includes all case facts, source references, coverage and decisions |
| request_result | `operation text`, `key uuid`, `request_sha256 text`, `response jsonb`, `created_at`; pk(operation,key); durable exact-request replay for review/freeze; mismatched reuse is 409 |
| audit_event | `id uuid pk`, `operation text`, `object_id uuid`, `correlation_id uuid`, `actor text fixed local_reviewer or worker`, `versions jsonb`, `created_at`; no raw notes, secret or source content |

Indexes: source_file(bundle_id,kind); source_row(source_file_id,row_no); case_record(run_id,case_key); decision(case_id,version desc); snapshot(run_id,review_version); run(bundle_id,rule_version); audit_event(object_id,created_at). Existing unique indexes satisfy overlapping lookups; do not duplicate them. No query-per-evidence-row: load one page's referenced rows in a bounded query.

Foreign keys use RESTRICT for history-bearing evidence; no cascade deletion that can erase frozen lineage. API and worker roles have no UPDATE/DELETE on immutable facts/source/snapshot/decision tables after migration; the worker role additionally has no INSERT on decision, snapshot or request_result and cannot change run.review_version; mutable run state/version and replay/audit writes use narrowly required grants. The coordinated migration role is separate configuration. Source/reference integrity is enforced before publication and before freeze; frozen payload references carry source hash/kind/row, not a browser-provided path.

### Transactions and ordering

- Upload: unique content_key chooses one accepted bundle; create its exactly three file references, normalized rows and run, and enqueue using the same node-postgres client via pg-boss `Db.executeSql`. On duplicate race, roll back loser staging and return the existing identity; changed manifest or bytes means a different bundle. Valid separate external transaction IDs are never collapsed by equal amount.
- Worker: pg-boss transactional worker owns result publication and completion together; all writes use its provided transaction adapter, not another pool. Unique run/case ownership is an additional safety net. If computation exceeds the configured deadline, fail/retry; never silently switch to nontransactional publication. Lost claim must roll back writes. Do not add an application `running` commit that can outlive an unrecorded failed attempt; UI derives active/retry status from the durable queue state plus run outcome.
- Review: begin, lock run row `FOR UPDATE`, validate case belongs to run, compare expected case version, append decision, increment run.review_version, append audit/replay result, commit. Lock order is run first, then case-associated records everywhere.
- Freeze: begin, lock same run row, verify completed and expected review_version, copy canonical sorted facts/evidence/decisions/coverage into snapshot, save replay/audit result, commit. A later review increments the aggregate and yields a new draft/version; old snapshot never mutates.
- Idempotency lookup happens before stale-version validation for a previously committed matching key, so a lost-response retry can return its original result even if newer reviews exist. A key with different request bytes is 409 `IDEMPOTENCY_CONFLICT`.

## 5. API Architecture

All `/api/v1` responses are JSON except download. IDs are UUID strings. All money is minor-unit integer strings with currency `usd`; reject JSON numeric money. Dates/timestamps are strings under the source contract. Success is `{data:<payload>}`. Errors are `{error:{code:string,message:string,correlation_id:uuid,details?:[{source?,row?,field?,code}]}}`; at most 50 detail entries plus `truncated:boolean` when applicable. Never return stack traces, local paths or secrets.

| Method/path | Request | Success payload | Failure codes/status |
|---|---|---|---|
| GET `/health` | None; no auth; no application data | 200 `{status:'ready'|'not_ready'}`; 503 not_ready when DB/schema incompatible | No secret/config dump |
| POST `/api/v1/bundles` | Multipart `manifest` JSON and exactly `stripe`,`bank`,`books` CSV files; contract SOURCE | 202 new `{bundle_id,run_id,state:'queued',reused:false}`; 200 identical accepted bundle `{bundle_id,run_id,state,reused:true}` | 400 MALFORMED_REQUEST; 413 LIMIT_EXCEEDED; 422 INVALID_SOURCE/MANIFEST; 503 DEPENDENCY_UNAVAILABLE |
| GET `/api/v1/bundles/:id` | None | `{id,manifest,sources:[{kind,sha256,bytes,row_count,preview:[{row_no,raw_fields}]} (preview max25 rows/source)],run_id}` | 404 NOT_FOUND |
| GET `/api/v1/runs/:id` | None | `{id,bundle_id,state,attempt,review_version,coverage,result_summary?,error_code?}`; state queued/running/retrying/failed/completed derived from durable queue and run | 404; 503 unavailable; never infer completed from missing queue row |
| GET `/api/v1/runs/:id/cases?after=&limit=` | limit integer 1..100 default25; after opaque validated key from same run | `{items:[Case],next_cursor:string|null,review_version}` sorted by stable case_key | 400 INVALID_CURSOR/LIMIT;404 |
| GET `/api/v1/cases/:id` | None | `Case` plus `evidence_rows:[EvidenceRow]`, `latest_decision:Decision|null`, `case_version:integer` | 404;409 EVIDENCE_INTEGRITY;503 |
| POST `/api/v1/runs/:id/retry` | JSON `{expected_job_id:uuid}`; `Idempotency-Key:uuid`; failed eligible transient job only | 202 `{run_id,job_id,state:'queued'}`; exact replay same | 404;409 NOT_RETRYABLE/STALE_VERSION/IDEMPOTENCY_CONFLICT |
| POST `/api/v1/cases/:id/decisions` | JSON `{expected_case_version:int>=0,disposition:'noted'|'needs_evidence',note:string<=2000}`; `Idempotency-Key:uuid` | 201 `{decision_id,case_version,run_id,review_version}`; matching replay returns same payload/status | 400 schema;404;409 STALE_VERSION/IDEMPOTENCY_CONFLICT |
| POST `/api/v1/runs/:id/snapshots` | JSON `{expected_review_version:int>=0}`; `Idempotency-Key:uuid` | 201 `{snapshot_id,run_id,review_version,payload_sha256}`; matching replay same | 404;409 RUN_NOT_COMPLETE/STALE_VERSION/IDEMPOTENCY_CONFLICT/EVIDENCE_INTEGRITY |
| GET `/api/v1/snapshots/:id` | None | `{id,run_id,review_version,payload_sha256,payload:Snapshot}` | 404;409 integrity |
| GET `/api/v1/snapshots/:id/export?format=html|csv` | Explicit format | 200 attachment `equivra-<snapshot UUID>.html|csv`, correct content type; fixed snapshot facts | 400 INVALID_FORMAT;404;409 integrity;503 EXPORT_UNAVAILABLE |

Common protected-route failures: 401 INVALID_ACCESS, 403 ORIGIN_REJECTED/HOST_REJECTED, 405 method, 415 unsupported content type, 500 INTERNAL_ERROR with safe correlation ID. State-changing GET is prohibited. Browser mutating routes require exact configured Origin and reject `null`; also reject `Sec-Fetch-Site: cross-site`. Do not rely on CORS to reject mutations. Unsupported methods/content types are rejected before any write. JSON request max64 KiB; multipart total max31 MiB, per file10 MiB, manifest64 KiB.

`Case={id,run_id,case_key,kind,evidence_state (supported|difference|incomplete|ambiguous|unsupported),facts,evidence:[{source_kind,row_no,source_sha256}],case_version}`. `EvidenceRow={source_kind,row_no,source_sha256,raw_fields,normalized}`. `Decision={id,version,disposition,note,created_at}`. `Snapshot={schema_version:'equivra.snapshot.v1',run_id,bundle_id,rule_version,review_version,manifest,source_hashes,cases:[Case with latest_decision],summary,coverage}`. All dynamic strings escaped at render; schema-defined maps/lists cannot contain arbitrary instructions or executable content. Every evidence reference is validated against its bundle.

Manual retry uses the documented run retry endpoint, preserving the approved eligible-retry workflow. Lock the run and require a terminal failed current job plus expected_job_id. Reject completed, active, queued, stale, malformed-input or integrity-failed runs as NOT_RETRYABLE/STALE_VERSION. A retryable dependency/interruption failure creates a new job ID in the same transaction as updating that run's current job_id/state; prior job/audit lineage stays intact. Queue payload still pins the same bundle/run/rule. Repeated matching Idempotency-Key returns the original queued response. Never reset a frozen report or accept a silent changed bundle. T07's queue adapter owns terminal-state observation and must prove the pinned library path without direct queue-table mutations.

### Deterministic evidence guidance — C-API UI contract

Approved addition on 2026-10-15: show “What this evidence shows” and “Next evidence check” in the case detail view. TASK-10 / T44 owns a fixed reason-code lookup inside future `web/src/App.tsx`; no new service, dependency, model call, endpoint, database field or snapshot field. Existing `facts.reason_code` selects the exact copy below. Display existing evidence state, amounts, source links and supplied-scope coverage alongside it. Never interpolate raw source strings into these messages or derive a financial conclusion from reviewer notes. These are investigation prompts, not accounting instructions or automatic actions.

| Reason code | What this evidence shows | Next evidence check |
|---|---|---|
| MATCHED_REFERENCE | The supplied reference and amounts support this relationship within the supplied scope. | No additional evidence is requested for this relationship; review the source rows and coverage before recording a disposition. |
| MISSING_BANK_EVIDENCE | No bank row links to this payout in the supplied export. | Check whether the bank export includes the payout reference and relevant posting period. |
| AMBIGUOUS_BANK_REFERENCE | Multiple supplied bank rows reference this payout. | Inspect the bank rows and obtain an unambiguous payout reference; do not select a row by amount alone. |
| UNLINKED_BANK_REFERENCE | This supplied bank row has no supported payout relationship. | Check its payout reference and the processor export coverage; equal amounts do not establish a link. |
| BANK_AMOUNT_DIFFERENCE | The explicitly linked bank amount differs from the supplied processor subtotal. | Inspect the linked rows and supplied coverage for omitted movements; the difference alone does not establish a loss. |
| MISSING_BOOK_EVIDENCE | This processor movement has no linked row in the supplied books export. | Check whether the books export includes this movement and its processor reference. |
| BOOK_AMOUNT_DIFFERENCE | The linked books total differs from the supplied processor movement. | Inspect all book lines with this processor reference and the supplied export coverage. |
| UNLINKED_BOOK_REFERENCE | This supplied books row has no supported processor relationship. | Check its processor reference and whether the referenced movement is included in the processor export. |
| UNSUPPORTED_CATEGORY | This supplied processor category is outside the supported investigation rules. | Inspect the original category and supported source profile; leave it unresolved rather than substituting another category. |
| MISSING_PAYOUT_MEMBERSHIP | The supplied movement lacks the payout membership needed for this relationship. | Check the source payout membership and export coverage; do not infer membership from amount or date. |
| PARTIAL_REFUND_IN_SUPPLIED_SCOPE | The identified supplied refunds do not exceed the linked original charge. | Review the original charge and refund rows; this does not establish bank settlement or refunded fees. |
| REFUND_EXCEEDS_SUPPLIED_CHARGE | The identified supplied refunds exceed the linked original charge. | Inspect the charge and refund references and supplied amounts before recording a conclusion. |
| MISSING_ORIGINAL_CHARGE | The supplied refund evidence lacks its linked original charge. | Check whether the processor export includes the original charge and its reference. |
| DISPUTE_REVERSAL_PRESENT | An identified dispute withdrawal and reversal are present in the supplied evidence; inspect their principal comparison. | Review both movements and their separate fees; this does not establish a dispute win. |
| UNPAIRED_DISPUTE_MOVEMENT | The supplied dispute movement lacks its identified partner. | Check the dispute identifier and whether the relevant withdrawal or reversal is included in the export. |
| AMBIGUOUS_DISPUTE_LINEAGE | The supplied dispute records do not establish one unambiguous withdrawal and reversal pair. | Inspect the dispute identifiers and candidate movements; a shared charge reference alone is insufficient. |
| CROSS_PERIOD_TIMING | The linked evidence has dates across the selected period boundary. | Review the distinct event, payout, bank and accounting dates and declared coverage; timing alone does not establish a loss. |

Unknown or absent code: show “No explanation is available for this evidence reason.” and “Inspect the source rows and supported source profile; leave the conclusion unresolved.” Do not render an untrusted code as HTML, change the evidence state, hide the case, or crash the view. Null observations/deltas remain visibly unknown. Explanation copy is presentation only and is not included in frozen HTML/CSV exports; existing snapshot facts/reason codes and report semantics remain unchanged. A future export-copy change requires its own report/version contract review.

Verification: T44's Node-driven Playwright suite must cover all 17 mappings using controlled case responses, unknown/absent codes, inert hostile source text, supported-state wording and no mutation/network call caused by displaying guidance. The real-provider S1 flow must show MISSING_BOOK_EVIDENCE guidance with expected -3000, observed/delta null and source links; saving a disposition must not change that guidance or evidence state. T46 / INT-03 repeats the real S1 assertion before accepting the browser journey. No added telemetry or migration. Rollback is UI-copy-only and preserves all evidence/review/snapshot history.

## 6. Auth & Permissions

The current code is generated with Node crypto on each API process start. Compare bounded Bearer values using a constant-time byte comparison after length validation. Do not expose code through `/health` or static files. Limit failed code attempts per remote loopback address with a bounded single-entry counter: 30 failures per60s returns429; reset on window expiry; it is process-local throttling, not distributed security. This does not replace Host/Origin checks. All protected reads/writes/downloads require current code.

The browser origin and allowed Host are exactly `127.0.0.1:4310`. Host-native mode binds127.0.0.1. The fixed Compose image binds0.0.0.0:4310 inside its isolated container so Docker forwarding works; Compose MUST publish `127.0.0.1:4310:4310`, never an all-interface host port. No user-selectable public bind, trusted proxy headers or cross-origin credentials. Integration verifies host exposure and denies hostile Host/Origin; container peer addresses are not treated as authentication. Static pages use CSP restricting script/connect to self and frame-ancestors none; source text is never innerHTML. Worker uses configured local DB/storage permissions and cannot create reviewer dispositions.

## 7. Background Jobs

Queue `equivra-investigate-v1`, payload `{schema_version:1,run_id:uuid,bundle_id:uuid,rule_version:'equivra.rules.v1'}`; no raw CSV content. Queue policy standard; application run uniqueness provides idempotence. RetryLimit2 (three total attempts), retryDelay2 seconds, exponential backoff enabled with max30s, expiration120s; transactional timeout125s; one job/handler, concurrency1; heartbeat30s if compatible with the selected PostgreSQL worker mode. DB statement timeout30s and lock timeout5s for ordinary API transactions; whole-request/upload deadline120s. These are safety bounds, not processing-speed SLAs.

Startup applies queue schema explicitly with the migration step; API/worker disable automatic queue migration during normal run. Configure queue retention to never silently erase the only durable state for an incomplete/failed application run; application failure reporting persists a sanitized terminal error separately before queue cleanup. T07 must verify actual supported retention/error hooks in pinned version and fail its intake gate if this guarantee cannot be represented. Do not improvise direct pg-boss table updates. completed application results/snapshots are never deleted by queue retention.

For the 10,000-row/source envelope, load a bounded normalized revision and use indexed maps, not pairwise amount searches. Domain output is computed deterministically. Transactional publication writes sorted case records and final run result in one commit with queue completion. Crash before commit rolls back all publication; crash after commit yields the same completed result. An older run may complete under its own identity but never replaces a selected newer bundle.

## 8. File Storage

`EQUIVRA_DATA_DIR` is an absolute server-owned directory outside static web assets; default local `.equivra-data/` with ignored data. Source storage key `<bundle UUID>/<kind>-<sha256>.csv` is generated, never taken from a submitted filename/path. Stage in a private directory, stream-limit/parse/hash before acceptance, fsync/rename into immutable storage before the accepting DB commit. Original source bytes remain available for lineage; no path is returned to the browser.

CSV: UTF-8 with optional BOM, comma delimiter, RFC4180 quoted fields/newlines, one header record, LF or CRLF. Reject duplicate headers, inconsistent columns, NUL/invalid UTF-8, field>4096 Unicode code points or record>32 KiB, missing/unknown required profile columns. Descriptions max2048 code points; external identifiers ASCII `[A-Za-z0-9_:-]{1,128}`. Source files must contain headers; valid header-only input is allowed with its declared coverage and explicit zero-observed-records status, never inferred evidence completeness. Zero-byte file is invalid.

## 9. Integrations and Financial Rules

No live integration or paid model. Stripe profile fields are inspired by the documented itemized automatic-payout report, but v1 accepts only the exact documented subset/synthetic fixtures; it is not a certification that every export/account/category works. Bank/books are Equivra synthetic profiles. Primary reference: [Stripe payout report](https://docs.stripe.com/reports/payout-reconciliation).

### Manifest v1

`{schema_version:'equivra.bundle.v1',workspace_id:'demo',source_account_id:'acct_demo',currency:'usd',period:{start:YYYY-MM-DD,end_exclusive:YYYY-MM-DD},coverage:{stripe:{start,end_exclusive},bank:{start,end_exclusive},books:{start,end_exclusive}}}`. Dates are real calendar dates, UTC interpretation, start<end, max370 days per range. Period must be contained in each declared coverage; adjacent-period evidence is permitted. These are supplied-scope declarations, not independent proofs that all activity was exported. Actual row event/posting dates must lie within their declared source coverage.

### Source schemas

| Source | Exact CSV headers and constraints |
|---|---|
| stripe | `balance_transaction_id,created_utc,available_on_utc,currency,gross,fee,net,reporting_category,automatic_payout_id,automatic_payout_effective_at_utc,source_id,charge_id` |
| bank | `bank_row_id,posted_on,currency,amount,payout_ref,description` |
| books | `entry_id,posted_on,currency,amount,processor_ref,description` |

Stripe `created_utc`, `available_on_utc`, `automatic_payout_effective_at_utc` are RFC3339 UTC strings ending Z. created/available required; payout-effective may be empty only when payout_id empty. bank/books posted_on is YYYY-MM-DD. currency must be usd. IDs balance_transaction_id/bank_row_id/entry_id are required and unique within their source; a duplicated ID is invalid even with equal values. Required nonidentity references may be empty and create an incomplete/unsupported relationship; never synthesize references from amounts.

Money accepts a signed decimal with up to10 integer digits and optional1–2 fractional digits, no exponent/thousands/currency symbols/whitespace; normalize to BigInt cents and preserve original text. Bound absolute row amount at9999999999.99 USD. `gross - fee == net` must hold exactly; failure is INVALID_MONEY_BRIDGE rather than an AI-correctable difference. Negative fees are accepted only as supplied exact source values, not invented refunds. Aggregate bounds fit signed64-bit cents for the approved row envelope; check before serialization/storage.

Stripe supported categories: `charge`, `refund`, `dispute`, `dispute_reversal`; all other valid categories remain `unsupported` evidence cases and prevent a claim that the affected payout lifecycle is fully supported. `source_id` identifies related processor object; charge_id groups original-payment lineage, not event identity. Dispute reversal needs an explicit supplied source/charge link; if its exact dispute reference cannot be established, show both movements and limited lineage without asserting same-dispute resolution. No heuristic charge-level identity substitutes for an absent dispute identity.

Books is **net activity in a synthetic processor clearing account**, not a general ledger export. Positive amount increases that clearing balance; negative decreases it. processor_ref must reference a Stripe balance_transaction_id for a supported direct relationship. Multiple book lines with the same processor_ref may sum to that event's net; preserve all entry_ids and compare exact signed totals. This profile excludes bank-transfer/payout-clearing journal lines so it does not double-count settlement. Unlinked or out-of-profile references remain unresolved; no accounting treatment is prescribed.

### Deterministic investigation v1

1. Group source Stripe rows by explicit automatic_payout_id; sum supplied net for a **subtotal of supplied rows**. Unknown categories/missing membership create coverage issues. Same-ID event conflicts reject source; distinct IDs survive equal values.
2. For a payout, candidate bank rows are exact nonempty payout_ref matches. One row with equal currency and amount supports the relation *within supplied scope*. Zero yields missing bank evidence; more than one yields ambiguity, never first match or automatic combination. A mismatched amount creates a difference with both source amounts, not a loss claim. Same-amount rows without a reference remain unlinked/ambiguous evidence; do not create allocations by amount/date.
3. For each Stripe balance event, exact processor_ref book lines sum to its supplied net. Zero linked rows yields missing book evidence; unequal sum yields difference; equal sum supports only that direct source relation. Extra/unreferenced books/bank rows remain explicit unlinked observations. Do not claim a zero subtotal proves complete books.
4. Refund partiality can be shown relative to explicitly linked original charge; sum identified refunds against supplied original gross, never assume original fee was refunded. A missing original charge limits interpretation.
5. Display supplied dispute withdrawal/reversal independently, with exact net movements; principal comparisons use supplied gross, fees separately. No permanent-loss or win inference from only a generic charge link.
6. Label timing using the distinct source dates and declared windows. No arbitrary days-of-tolerance auto-match. A reference and amount can support an adjacent-window relation while its dates differ; missing adjacent evidence stays incomplete.
7. Output sorted deterministic case keys and evidence rows. Supported relations and reviewer dispositions are separate fields. Run coverage always states `supplied_scope_only`; complete run means computation completed, not real financial completeness.

### Case taxonomy and exact comparison semantics

Kinds: payout_bank, event_books, unlinked_bank, unlinked_books, unsupported_category, refund_lifecycle, dispute_lifecycle, timing. States: supported, difference, incomplete, ambiguous, unsupported. Summary contains a count for each state plus cases_total. For an exact amount comparison with both values present, delta_minor=observed_minor-expected_minor; unequal known amounts use difference, never missing-evidence classification. If observed evidence is absent, observed_minor and delta_minor are null, not zero. Lifecycle metadata need not be a monetary comparison: delta_minor=null when no comparison is meaningful.

Reason codes: MATCHED_REFERENCE, MISSING_BANK_EVIDENCE, AMBIGUOUS_BANK_REFERENCE, UNLINKED_BANK_REFERENCE, BANK_AMOUNT_DIFFERENCE, MISSING_BOOK_EVIDENCE, BOOK_AMOUNT_DIFFERENCE, UNLINKED_BOOK_REFERENCE, UNSUPPORTED_CATEGORY, MISSING_PAYOUT_MEMBERSHIP, PARTIAL_REFUND_IN_SUPPLIED_SCOPE, REFUND_EXCEEDS_SUPPLIED_CHARGE, MISSING_ORIGINAL_CHARGE, DISPUTE_REVERSAL_PRESENT, UNPAIRED_DISPUTE_MOVEMENT, AMBIGUOUS_DISPUTE_LINEAGE, CROSS_PERIOD_TIMING. Case keys follow C-DOMAIN. An unlinked bank row with an amount equal to a payout but no ref remains ambiguous/unlinked; it never consumes an allocation.

Refund lifecycle: for supplied original charge_id, compare sum of absolute negative identified refund gross values with positive original charge gross. At or below original is supported supplied-scope refund metadata, not a bank match; greater is difference. Missing original is incomplete. Do not compare fees as if refunded unless supplied. Dispute lifecycle: only source_id explicitly beginning dp_ plus exactly one withdrawal and one reversal of the same dispute can support reversal-present metadata; gross principal total zero is supported and nonzero is difference. Absent partner is incomplete, multiple candidate withdrawal/reversal records or only a shared charge_id is ambiguous. All underlying movements remain visible; none is labeled a permanent loss or a dispute win. Temporal case uses explicitly linked payout/deposit dates, not a heuristic matching tolerance.

## 10. Observability

Structured request/job logs: operation, correlation_id, bundle/run/job/snapshot IDs, outcome, error code, attempt and duration. Redact auth headers, code, note/source strings and DB URL. Existing UI job/run states are the day-one local dashboard; no additional monitoring service. Failure code and correlation ID remain visible. Audit review/freeze separately without raw note text in operational logs.

## 11. Deployment Assumptions

Local initialization: CREATE `scripts/init-local.mjs` (stdlib only) generates API/worker/migration database passwords and owner-only `.env` without printing secrets; refuses overwrite of an existing config. Its command `npm run init:local` runs before container start, supports the inspected Node25 host as a setup utility, and does not alter global runtimes. Compose consumes generated local credentials, keeps DB host binding loopback, and provides writable server-owned source storage. The migration tool creates restricted runtime roles safely with server-quoted generated credentials; SQL files never contain passwords. These operations must be tested in a temporary project/config directory.

Config: `DATABASE_URL` (API role), `WORKER_DATABASE_URL` (worker role), `MIGRATION_DATABASE_URL` (migration role), `EQUIVRA_DATA_DIR`, fixed port4310 and immutable build/rule/profile version constants; fixed host-native/Compose binding profiles only, no arbitrary host/interface setting in v1. Database URLs allow only loopback hosts or the fixed Compose service hostname db on the application-owned local network at startup, no remote unapproved resource. Compose publishes DB only on127.0.0.1, persists volume; do not run down -v as a recovery step. CI uses disposable local PostgreSQL and synthetic fixtures. App migrations and pg-boss install precede matching API/worker start. Upgrade/rollback stops both and restores compatible DB+files; never mutate old snapshots to accommodate a newer renderer.

## 12. System Boundaries & Contracts

See [contract registry](contracts/registry.md) for full provider/consumer records and fixtures. All source/code paths are CREATE until implemented. Contracts may be design-frozen once schema, errors and fixtures pass static review; executable freeze additionally requires provider conformance and T01 command-gate evidence. Breaking a frozen contract requires updating every consumer, fixtures, affected packets and DAG, not a private response change.

## 13. Parallelization Map

Freeze source/runtime/API fixtures before consumers. After foundation and data types, ingestion, pure domain rules, and UI can start against pinned contracts/fixtures; they cannot merge to a complete application before real provider checks. Shared DB schema is owned by one task; API route assembly is serialized after access and feature handlers. Worker publication and freeze/review concurrency are architect-review-required. Exact DAG/waves are in [orchestration](orchestration.md).

## 14. Risk Register

| Risk | Likelihood/impact | Proof / escalation |
|---|---|---|
| Source profile mistaken for universal export support | Medium/High | Fixture/schema docs and UI label synthetic bank/books and supplied-scope-only; stop unsupported assumptions |
| Dispute identity missing in selected report | High/Medium | Keep unsupported/incomplete lineage; do not infer a dispute win or same-dispute relationship from amount/charge alone |
| Transaction adapter not compatible with pinned library | Medium/High | T01/T07 live local enqueue rollback/completion probes; architect changes contract on failure |
| API/worker half-commits or stale owners | Medium/High | Real PostgreSQL interruption/concurrency tests, not mocked transaction functions |
| Auth code stored/logged or browser boundary bypass | Medium/High | Missing/old code, hostile Origin/Host, redaction and memory-only browser checks |
| Immutable report reads mutable facts | Medium/High | Render snapshot payload only; correction/review scheduling test and archive restore |
| Foundations absent | Certain/High for readiness | No unit/build/test commands are currently verified; T01 gates every implementation consumer |

No production readiness, benchmark success, paid demand or general accounting correctness is claimed by this written design.
