# TASK-10 — Build the complete accessible local React investigation journey

Status: future implementation packet. Coding authorization and G0/provider gates are not passed. TASK-01 owns bootstrap/G0 and may start only after coding authorization; downstream packets wait the declared handoffs. No done claim.

**Objective**
Build the complete accessible local React investigation journey.

**Why this task exists**
Own the approved Web outcome without weakening money/evidence/version/access/recovery guarantees. No extra product scope.

**Workstream / execution wave**
Web, W2 (start wave, not merge permission).

**Depends on**
- TASK-01 via C-FOUNDATION,C-API; start=G0 + design-frozen shapes and fixtures; merge=Provider executable conformance for C-FOUNDATION,C-API
- TASK-02 via C-SOURCE; start=G0 + design-frozen shapes and fixtures; merge=Provider executable conformance for C-SOURCE
- TASK-04 via C-ACCESS; start=G0 + design-frozen shapes and fixtures; merge=Provider executable conformance for C-ACCESS
- TASK-08 via C-REVIEW; start=G0 + frozen review shape/mock; provider implementation needed for merge; merge=Provider executable conformance for C-REVIEW
- TASK-09 via C-REPORT; start=G0 + frozen snapshot/export fixture; provider implementation needed for merge; merge=Provider executable conformance for C-REPORT
- INT-02 via ; start=G0 + fixed API/access/review/report fixtures permit W2 start; merge=INT-02 actual API provider conformance passed

**Blocks / consumers**
- INT-03 via INT-03

**Inputs**
Approved PRD/design; repo_context verified baseline; architecture and S1-S8 scenario definitions; complete consumed/produced contract records copied below. No provider-private implementation knowledge.

**Outputs**
Owned files, required behavior/conformance tests, and recorded verification outcomes; only produced contracts may be declared executable-frozen after passing checks.

**Files to inspect first**
- docs/repo_context.md — baseline/actual command evidence.
- docs/architecture.md — authoritative schema/API/source/financial/transaction design.
- docs/demo-scenarios.md; docs/contracts/examples/manifest.json, stripe.csv, bank.csv, books.csv, books-corrected.csv, expected.json, api-responses.json and snapshot.json — existing explicitly synthetic examples.
- This packet. Premium rule root: /Users/mac/.codex/plugins/cache/personal/premium-product-builder/0.1.0/skills/premium-product-builder/. Named rules relative to that root: security_rules.md, testing_rules.md, product_quality_bar.md; backend_rules.md/api_rules.md/database_rules.md for those boundaries, frontend_rules.md for UI. Skill rules cannot expand approved scope.

**Owned files**
- CREATE web/src/App.tsx
- CREATE web/src/api.ts
- CREATE web/src/styles.css
- CREATE tests/e2e/workbench.test.ts

**Non-owned / do-not-touch files**
All files outside the owned list.
- package.json — another packet or architect owns it; no casual contract edits.
- package-lock.json — another packet or architect owns it; no casual contract edits.
- db/001_initial.sql — another packet or architect owns it; no casual contract edits.
- server/app.ts — another packet or architect owns it; no casual contract edits.
- server/worker.ts — another packet or architect owns it; no casual contract edits.
- docs/contracts/registry.json — another packet or architect owns it; no casual contract edits.
- .git/, .gstack/, .codex/, .agents/ and external attachments — no edits. Shared files may change only in the explicitly serialized owner stage.

**Scope**
Only the objective, owned files and steps below; retain all approved source/money/access/version/uncertainty constraints.

**Out of scope**
Real data, hosting, SaaS accounts, AI/live connectors, payment/accounting writes, universal formats and unrelated features.

**User-facing behavior**
For source/domain/storage-only work: internal prerequisite surfaced by later declared UI/API. For access/import/review/report/web: exactly the methods/states in copied C-API and the acceptance criteria, no extra flow.

**Data model**
Full C-DB record pasted below when consumed/produced; otherwise N/A — no DB schema ownership. Only TASK-03 may change the initial schema.

**API contract**
Full C-API and provider-specific record pasted below when consumed/produced; otherwise N/A — no HTTP surface in this pure/foundation task.

**UI states**
N/A for pure/internal-only task. Browser-facing behavior must distinguish loading, empty, validation/dependency error, success, incomplete/ambiguous/difference, stale conflict and unavailable access; never hide uncertainty. Exact field/error mappings are the copied wire contract.

**Validation rules**
Use complete copied source/API limits and enums. Common safe message mapping: INVALID_ACCESS=Enter the current local startup code.; STALE_VERSION=Evidence or review changed; reload before submitting.; INVALID_SOURCE=Invalid source; review the named field details.; LIMIT_EXCEEDED=Source exceeds the supported input limit.; DEPENDENCY_UNAVAILABLE=Local dependency unavailable; retry when restored.; INTERNAL_ERROR=Operation failed; use the correlation reference. Do not echo raw value/path/secret. Other code-specific messages name the failed operation and action without guessing facts.

**Auth & permissions**
C-ACCESS current-start local reviewer gate before application routes; worker restricted role only. Protected data may not be read from health/static shell or unguarded route.

**Integration contract**
Complete provider/consumer records below are the only handoff. No private source knowledge; compatibility/versioning and fixture change protocol binding.

**Manual QA**
After G0 and provider readiness, use the documented synthetic bundle. For internal tasks run their declared behavior test and inspect expected facts/errors. For browser/API tasks exercise success plus one invalid/unauthorized/stale/failure branch and verify visible recovery. At convergence walk S1 then S4/S6/S7; compare6680 subtotal and missing refund evidence, never claim current application behavior before implementation.

**Do not change**
No files outside ownership, no approved behavior/limits or frozen contract without architect change record. No history deletion or external publication.

**Contracts consumed**
C-FOUNDATION, C-SOURCE, C-ACCESS, C-API, C-REVIEW, C-REPORT

**Contracts produced**
N/A — runtime/UI/checkpoint implementation consumes the existing protocol, no new public contract.

**Implementation steps**
1. Access, three-source upload/preview, durable status/cases, evidence/review and freeze/export views; native React/fetch, no generic KPI feature.
2. Code in memory only; refresh/new tab entry;401 clears access.409 preserves draft and asks deliberate reload instead of auto-resubmission.
3. Explicit loading/empty/error/success/partial states, semantic labels/tables/focus/status, readable long refs and stacked narrow-screen panels.
4. Start from frozen mock fixtures after G0; runtime merge waits INT-02 conformance, not mock-only success.

**Invariants affected**
- INV-01: Only the current-start code may access application data/actions; loopback/Host/Origin enforced; worker cannot insert reviewer decisions/snapshots.
- INV-05: Review and freeze serialize against the same owning run; expected versions reject stale changes; exact-request replay returns the original committed result.
- INV-06: Frozen snapshot captures all cases/facts/evidence/decisions; renderer uses that payload only; later corrections/reviews never change old facts.
- INV-07: Incomplete/ambiguous/unsupported evidence remains explicit; a reviewer disposition or balanced supplied subtotal cannot prove complete real books.
- INV-08: Enforce10000 data rows/10MiB per source and bounded parsing/errors; source text inert; secrets/raw rows absent from logs.

**Failure/error semantics**
Apply exact named errors in copied contracts: invalid input422/400/413, access401/403/429, missing404, stale/replay/integrity409, dependencies503, unexpected500 safe correlation. Known uncertainty is an evidence state, not an empty success. Roll back rejected writes; never silently coerce money, truncate sources, overwrite history or complete failed jobs.

**Security/privacy**
Synthetic-only. Parameterized SQL, generated storage identifiers, owning-revision links, source text escaped, startup code/raw financial text redacted. Current access/Origin/Host before browser mutation. Worker cannot invent reviewer decisions or move money.

**Observability**
Runtime owner emits operation/correlation/bundle/run/job/snapshot IDs, outcome/error/attempt/duration with no raw text/secrets. Pure source/domain functions return typed diagnostics; caller logs once. No new monitoring vendor.

**Migration/backfill/compatibility**
TASK-03 owns initial schema. Others consume its constraints unchanged. No real-data backfill. V1 source/rule/API/snapshot changes follow architect change protocol and update all fixtures/consumers. Preserve immutable history; coordinated compatible rollback only.

**Required tests**
- Node-driven Playwright full real API/worker/PG import->refund evidence->review->freeze->download.
- Invalid/current/previous access and no persistent secret/URL; source errors, queued refresh, stale saves/freezes, eligible retry, zero-case coverage.
- Keyboard/focus/narrow-screen amounts/references usable and source strings inert in actual DOM/download.
- Regression: retain every relevant S1-S8 accepted money/uncertainty/replay/correction/review/report/access bound; no old tests exist to retire.

**Verification commands**
Current repository application commands: NONE verified. Host versions were inspected but do not prove Node24. After TASK-01 G0, exact proposed scripts are npm run typecheck, npm run build, npm run test:unit, npm run test:integration, npm run test:e2e, npm run db:migrate as applicable under pinned Node24 local environment. They are specifications until created/inspected/invoked and recorded in repo_context. Missing/failed/zero-test suite is not acceptance. Run the behavior-specific families listed above; do not broaden unrelated suites without cause.

**Acceptance criteria**
1. PASS/FAIL: Critical journey passes real providers and frozen wire protocol.
2. PASS/FAIL: All declared states explicit/actionable; uncertainty and review disposition remain separate.
3. PASS/FAIL: No token in storage/URL/log; conflicts keep draft.
4. PASS/FAIL: Frozen output shows correct evidence and remaining unknowns.

**Rollback / recovery**
Revert UI only against compatible API; preserve sources/reviews/snapshots, no server workaround hidden in frontend.

**Downstream handoff**
Give consumer the frozen shape/examples/error/version/ownership semantics copied below plus actual provider conformance. It must not need provider-private code. Mark every unverified contract not-yet-consumable and block merge. Runtime-only packets hand off checkpoint evidence without changing the protocol.

**Definition of done**
All owned code/tests/docs/config complete; all numbered criteria and applicable verified commands pass; produced contracts executable-frozen or explicitly blocked; no hidden design choice assigned to builder; unrelated files untouched. This packet is not currently implemented.

**Effort**
2.5 engineer days at8h/day, preliminary sizing <=3-day cap; main cost is behavior/integration verification. TASK-01 is an atomic bootstrap exception to the usual small file count: splitting required runtime/type/mock configuration into file-only tickets would not yield independent outcomes. Calendar pace is10h/week; no measured AI speedup or completion promise.

## Complete handoff contract records

### C-FOUNDATION — Runtime and verification interface

**Provider Component**
Foundation

**Provider Task**
TASK-01

**Consumers**
TASK-02, TASK-03, TASK-04, TASK-05, TASK-06, TASK-07, TASK-08, TASK-09, TASK-10, TASK-11, TASK-12

**Type**
runtime/config/commands

**Source Of Truth**
docs/architecture.md sections 1-3 and CREATE package.json, package-lock.json, tsconfig.server.json, web/package.json, Dockerfile, compose.yaml

**Inputs**
Node24 container baseline; local PostgreSQL18; DATABASE_URL local/test-only; EQUIVRA_DATA_DIR server-owned; loopback API127.0.0.1:4310. Separate API/worker/migration DB URLs; allow loopback or fixed Compose hostname db, not arbitrary remote hosts. Disposable tests require name equivra_test_<random hex>; never reset the primary DB.

**Outputs**
Pinned package/lockfile; ESM TypeScript build; script names typecheck, build, test:unit, test:integration, test:e2e, verify, db:migrate, start:api, start:worker. Host Node25 is not baseline proof.
Exact proposed package scripts (not current verified commands):
{
  "typecheck": "tsc --noEmit -p tsconfig.server.json && tsc --noEmit -p web/tsconfig.json",
  "build": "tsc -p tsconfig.server.json && npm --workspace web run build",
  "test:unit": "node --test dist/tests/unit/*.test.js",
  "test:integration": "node --test --test-concurrency=1 dist/tests/integration/*.test.js",
  "test:e2e": "node --test --test-concurrency=1 dist/tests/e2e/*.test.js",
  "verify": "npm run typecheck && npm run build && npm run test:unit && npm run test:integration && npm run test:e2e",
  "db:migrate": "node dist/db/migrate.js",
  "start:api": "node dist/server/main.js",
  "start:worker": "node dist/server/worker.js"
}
Test scripts must fail on absent suites; G0 records command definitions and the executable readiness of each family separately. Integration requires a disposable local test DB; browser tests use Playwright library under the Node runner. No automatic zero-test PASS. init:local = node scripts/init-local.mjs; generated .env must be0600, no overwrite/secret print; setup utility may run on host Node>=22 while actual app checks use Node24 container. Shared pure canonicalJson(value: JSONValue):string sorts object keys recursively, preserves array order, emits compact UTF8 JSON with ordinary JSON string escaping; disallow non-JSON/unsafe numeric values. CREATE shared/canonical.ts, used for bundle, request and snapshot hashes. Runtime symbols: server/config.ts loadConfig(env):AppConfig; server/db.ts openDb(url):Pool and withTransaction(pool, fn(client)):Promise<T>; server/app.ts createApp(config,deps:{db:Pool,boss:PgBoss}):Promise<FastifyInstance>. All app money remains strings.

**Preconditions**
No application currently exists. TASK-01 may create only its owned foundation files after implementation authorization.

**Postconditions**
Record exact commands and observed outcomes in docs/repo_context.md. Reject public host publication and wrong DB/test targets; ignore generated data/build/secret directories.

**Error Semantics**
Bad config or incompatible schema/runtime fails startup; never fall back to a remote database/public bind. Missing test families cannot be reported passing.

**Idempotency Retry**
Clean setup repeatable; no automatic destructive reset. migrations serialized.

**Ordering Concurrency**
Own shared root configuration once; later tasks may not casually edit scripts/lockfile.

**Fixture**
docs/contracts/examples/* existing data; CREATE tests/support/mock-api.ts during TASK-01 for the fixed API shapes in C-API.

**Freeze Point**
G0: package script definitions, pinned runtime/dependencies and command invocation results recorded; downstream command readiness remains blocked until this evidence exists.

**Verification**
Current verified host commands: node --version=v25.8.1, npm --version=11.11.0, docker --version=29.0.1, git --version=2.50.1. Planned commands are not repo-verified today. G0 must inspect package scripts and run defined checks in the selected Node24 environment.

**Lifecycle**
v1 is design-frozen after this plan review; executable freeze requires provider conformance and foundation evidence. No implicit backward-incompatible changes.

**Change Protocol**
Identify every consumer; update this record, examples, generated/typed interfaces, affected packets and edges; rerun conformance; re-sequence before merging a breaking change.

**Security**
Local synthetic demo only; protect application routes with current startup code, exact Host/Origin and owning-revision validation. Never expose secrets or local paths.
Binding contract: browser origin/Host127.0.0.1:4310; host-native listener127.0.0.1 only. Fixed Compose image listener0.0.0.0:4310 is internal only and MUST use host publication127.0.0.1:4310:4310; never public host publication. Reject arbitrary bind configuration. Docker peer IP is not authentication; Host/Origin/Bearer remain mandatory. Test published host interfaces and deny hostile Host/Origin.

### C-SOURCE — Three source profiles and exact normalization

**Provider Component**
Source ingestion

**Provider Task**
TASK-02

**Consumers**
TASK-03, TASK-05, TASK-06, TASK-07, TASK-09, TASK-10, TASK-11, TASK-12

**Type**
file/schema/function

**Source Of Truth**
docs/architecture.md sections 8-9; examples/manifest.json,stripe.csv,bank.csv,books.csv,books-corrected.csv,expected.json; CREATE shared/source.ts, shared/money.ts

**Inputs**
Manifest schema_version equivra.bundle.v1, workspace_id demo, source_account_id acct_demo, currency usd, period and per-source half-open date coverage. Exact header arrays in architecture section9. UTF8 CSV, at most10000 data records and10485760 bytes/file; field4096 codepoints, description2048, record32768 bytes. Dates real UTC/RFC3339Z or YYYY-MM-DD as specified. External IDs ASCII [A-Za-z0-9_:-]{1,128}.
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



**Outputs**
ParsedSource={kind:stripe|bank|books,sha256,bytes,row_count,rows:[{row_no,raw_fields,normalized}]}; raw_fields maps exact headers to original strings. Stripe normalized fields preserve IDs/dates/category and gross_minor,fee_minor,net_minor integer strings; bank normalized amount_minor and payout_ref; books normalized amount_minor and processor_ref. parseMoney(decimal:string):string returns signed cents (no exponent; <=10 integer digits,<=2 decimals). Exports validateManifest(value:unknown):Manifest, parseMoney(decimal:string):string and parseSource(kind, bytes:AsyncIterable<Uint8Array>, coverage):Promise<ParsedSource>; callers may not depend on parser private helpers.

**Preconditions**
All three kinds supplied; manifest range start<end_exclusive and <=370 days; period lies in each coverage; each row date inside its declared coverage. No filename/path used as storage authority.

**Postconditions**
Exact gross-fee=net; no unsafe rounding. Header-only source accepted as zero observations with explicit coverage warning; zero-byte/malformed source rejected. Distinct external IDs survive identical amounts; duplicate source identity rejected. No claim of actual complete financial records.

**Error Semantics**
422 INVALID_MANIFEST, INVALID_SOURCE, INVALID_UTF8, INVALID_MONEY_BRIDGE, DUPLICATE_SOURCE_ID, UNSUPPORTED_CURRENCY;413 LIMIT_EXCEEDED; diagnostics<=50 entries plus truncated flag, no accepted partial bundle.

**Idempotency Retry**
Pure normalization repeatable; SHA covers original bytes. Corrected full bundle creates new revision; raw source never edited.

**Ordering Concurrency**
No state mutation. Stable row_no refers to logical CSV record after header, including quoted multiline fields as one record.

**Fixture**
Existing example bundle/expected.json plus corrected-books example; TASK-02 must create remaining S2-S8 cases before their consumers merge.

**Freeze Point**
Design shape now; executable parser/fixture conformance after TASK-02. Consumer may use documented example and schema before provider internals.

**Verification**
Unit table cases for exact money, Unicode/CSV limits, malformed/empty source, duplicate identity; existing example must yield6680 payout subtotal and incomplete refund books evidence. Planned npm run test:unit after G0; never assert it ran now.

**Lifecycle**
v1 is design-frozen after this plan review; executable freeze requires provider conformance and foundation evidence. No implicit backward-incompatible changes.

**Change Protocol**
Identify every consumer; update this record, examples, generated/typed interfaces, affected packets and edges; rerun conformance; re-sequence before merging a breaking change.

**Security**
Local synthetic demo only; protect application routes with current startup code, exact Host/Origin and owning-revision validation. Never expose secrets or local paths.

### C-ACCESS — Local current-start access and browser boundary

**Provider Component**
Local API access

**Provider Task**
TASK-04

**Consumers**
TASK-05, TASK-07, TASK-08, TASK-09, TASK-10, TASK-11, TASK-12

**Type**
HTTP/config/security

**Source Of Truth**
docs/architecture.md section6; CREATE server/access.ts; serialized registration into server/app.ts

**Inputs**
Authorization: Bearer <current 32-random-byte base64url code>; Host127.0.0.1:4310; exact Origin http://127.0.0.1:4310 on browser mutations; reject null/cross-site; JSON64KiB, multipart31MiB limits.

**Outputs**
Current code permits protected route processing, not a data/ownership bypass. Static shell and minimal /health are unauthenticated with no application data. Code enters browser memory only; refresh/new tab requires re-entry; API restart invalidates previous code. Export registerAccess(app:FastifyInstance, config:{startup_code:string,origin:string,host:string}):Promise<void>; mounts protected-prefix hook before feature routes.

**Preconditions**
API binds loopback only, does not trust forwarding headers; startup shows code intentionally in terminal, never structured logs, URL or file.

**Postconditions**
Missing/wrong/old code denied; proper Origin/Host still required with valid code; all application reads/actions/downloads protected. No SaaS accounts or real-data claim.

**Error Semantics**
401 INVALID_ACCESS,403 ORIGIN_REJECTED/HOST_REJECTED,429 after30 failed attempts/60s; safe generic response. Constant-time equal-length comparison; do not echo submitted code.

**Idempotency Retry**
New code per API start; no persistent sessions/cookies/storage; no automatic mutation retries after401.

**Ordering Concurrency**
Guard at global protected-route boundary before domain/parser work; worker internal DB access is not a browser session.

**Fixture**
CREATE tests/support/access.ts fixtures for a current/wrong/previous code, allowed/disallowed origins and hosts; consumer tests use injected application runtime code through normal config wiring.

**Freeze Point**
Executable freeze after TASK-04 negative/current restart tests; UI can start from documented responses after G0 mock fixture.

**Verification**
API negative/positive cases and Node-driven browser test: reload code entry, no storage/URL/log leaks, cross-site mutation forbidden. Planned unit/integration/e2e families after G0.

**Lifecycle**
v1 is design-frozen after this plan review; executable freeze requires provider conformance and foundation evidence. No implicit backward-incompatible changes.

**Change Protocol**
Identify every consumer; update this record, examples, generated/typed interfaces, affected packets and edges; rerun conformance; re-sequence before merging a breaking change.

**Security**
Local synthetic demo only; protect application routes with current startup code, exact Host/Origin and owning-revision validation. Never expose secrets or local paths.
Binding contract: browser origin/Host127.0.0.1:4310; host-native listener127.0.0.1 only. Fixed Compose image listener0.0.0.0:4310 is internal only and MUST use host publication127.0.0.1:4310:4310; never public host publication. Reject arbitrary bind configuration. Docker peer IP is not authentication; Host/Origin/Bearer remain mandatory. Test published host interfaces and deny hostile Host/Origin.

### C-API — Browser/API wire protocol and UI state handoff

**Provider Component**
Protocol foundation

**Provider Task**
TASK-01

**Consumers**
TASK-04, TASK-05, TASK-07, TASK-08, TASK-09, TASK-10, TASK-11, TASK-12

**Type**
HTTP/UI/schema

**Source Of Truth**
docs/architecture.md section5; CREATE shared/api.ts (initial interface owned TASK-01; runtime provider TASK-11), server/app.ts (serial assembly)

**Inputs**
Exact method/path/body/header/query definitions in architecture section5, including full bundle multipart, paginated run cases, expected-version decision/freeze, eligible failed-run retry and frozen export. Idempotency-Key UUID required for decision/freeze/retry.
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



**Outputs**
JSON {data:payload}; errors {error:{code,message,correlation_id,details?,truncated?}}. UUID IDs; minor amounts strings; null represents absent observed/delta evidence. Case/EvidenceRow/Decision/Snapshot exact shapes in architecture section5. TASK-01 owns the shared wire shape/mock freeze; TASK-11 assembles runtime providers and proves conformance, not a competing schema owner. Facts={currency:usd,expected_minor:string|null,observed_minor:string|null,delta_minor:string|null,reason_code:enum defined in architecture9,references:{payout_id?,balance_transaction_id?,charge_id?,dispute_id?}}. Evidence states supported|difference|incomplete|ambiguous|unsupported. Run result_summary={cases_total,supported,difference,incomplete,ambiguous,unsupported}; coverage={basis:supplied_scope_only,observed_rows:{stripe,bank,books},warnings:[code]}; attempt is0 before claim then positive. Multi-query read responses use one read-only repeatable snapshot, not mixed latest queries. Assembly calls registerAccess, registerImportRoutes, registerJobRoutes, registerReviewRoutes, registerReportRoutes in that order, then serves built static UI. No protected handler is mounted outside access hook. JSON reads needing several SQL statements use one read-only repeatable snapshot. Errors always place truncated inside error, not the outer envelope.

**Preconditions**
C-ACCESS and ownership guards; frozen doc/examples plus TASK-01 mock fixture before UI starts. All future symbols marked CREATE, not existing implementation.

**Postconditions**
No body data on invalid access, no silent partial-complete, no stale override, no bare report generated from current mutable state. limit1..100 default25; source refs validated under owning revision.

**Error Semantics**
400 malformed/schema/query,401 access,403 origin/host,404 missing ID,409 stale/replay/integrity/not-retryable,413 bounds,415 content type,422 source invalid,429 access throttle,500 safe unknown,503 unavailable. UI retains draft and shows recovery action; never retries stale save automatically.

**Idempotency Retry**
Stable bundle replay; exact key+request replay for decisions/freeze/retry; mismatched key body409. Read-only GETs idempotent; exports from frozen snapshot.

**Ordering Concurrency**
Review and freeze serialize on run lock/aggregate version, both completion orders verified; correction creates separate immutable bundle. No implicit latest-pointer reassignment by stale job.

**Fixture**
Existing source example plus existing docs/contracts/examples/api-responses.json and TASK-01 tests/support/mock-api.ts fixed normal/error responses; runtime conformance requires real providers.

**Freeze Point**
Design wire contract now; TASK-01 interface/mock freeze permits UI start after G0; TASK-11 runtime conformance and INT-02 required to merge UI integration.

**Verification**
Provider/consumer wire fixtures, all listed error mappings and real end-to-end API boundary tests; planned test:integration then test:e2e after G0. A mock-only UI check does not prove provider agreement.

**Lifecycle**
v1 is design-frozen after this plan review; executable freeze requires provider conformance and foundation evidence. No implicit backward-incompatible changes.

**Change Protocol**
Identify every consumer; update this record, examples, generated/typed interfaces, affected packets and edges; rerun conformance; re-sequence before merging a breaking change.

**Security**
Local synthetic demo only; protect application routes with current startup code, exact Host/Origin and owning-revision validation. Never expose secrets or local paths.

### C-REVIEW — Expected-version saved dispositions

**Provider Component**
Evidence review

**Provider Task**
TASK-08

**Consumers**
TASK-09, TASK-10, TASK-11, TASK-12

**Type**
HTTP/storage/function

**Source Of Truth**
docs/architecture.md sections4-5; CREATE server/reviews.ts

**Inputs**
Case UUID, expected_case_version integer>=0, disposition noted|needs_evidence, note<=2000 codepoints; Idempotency-Key UUID; current access and owning-run identity.

**Outputs**
201 {decision_id,case_version,run_id,review_version}; exact matching committed replay returns same response; Case read shows latest Decision or null plus version0 when unreviewed. Export registerReviewRoutes(app,deps:{db:Pool}):Promise<void>; owns case list/detail and disposition routes. Multi-query reads use one read-only repeatable snapshot so latest decision/version fields agree.

**Preconditions**
C-DB run-first row locking and C-ACCESS/C-API boundary; completed owning run and fixed case facts.

**Postconditions**
Append exactly one decision successor; increment run.review_version atomically; no financial source mutation and no implicit freeze.

**Error Semantics**
400 invalid input;401/403 access/browser;404 missing case;409 stale or mismatched replay key;503 DB unavailable; no write on error.

**Idempotency Retry**
request_result lookup for matching operation/key/hash before stale comparison; different request hash409; lost response safe to repeat exact key.

**Ordering Concurrency**
Lock owning run FOR UPDATE before comparing latest case decision version. Both reviewer orders produce one successor and conflict for loser; same run lock coordinates freeze.

**Fixture**
C-API wire examples; CREATE saved-review seed/response fixture in TASK-08, before TASK-09/TASK-10 merge.

**Freeze Point**
Shape frozen from architecture; executable conformance after TASK-08 real DB conflicting writes and replay check.

**Verification**
Integration: competing equal-version writers, save-before-freeze/freeze-before-save schedules, cross-run ID denial and no snapshot produced by save. Commands planned until G0.

**Lifecycle**
v1 is design-frozen after this plan review; executable freeze requires provider conformance and foundation evidence. No implicit backward-incompatible changes.

**Change Protocol**
Identify every consumer; update this record, examples, generated/typed interfaces, affected packets and edges; rerun conformance; re-sequence before merging a breaking change.

**Security**
Local synthetic demo only; protect application routes with current startup code, exact Host/Origin and owning-revision validation. Never expose secrets or local paths.

### C-REPORT — Versioned review, atomic snapshot and safe report

**Provider Component**
Review/workpaper

**Provider Task**
TASK-09

**Consumers**
TASK-10, TASK-11, TASK-12

**Type**
snapshot/function/HTTP

**Source Of Truth**
docs/architecture.md sections4,5,9; CREATE server/reviews.ts (TASK-08),server/reports.ts,shared/report.ts (TASK-09)

**Inputs**
Completed run; expected review aggregate version; snapshots capture manifest/source hashes, rule_version, all sorted case facts/evidence and latest saved decisions. Review changes append version; freeze explicit, not implicit in save.

**Outputs**
Snapshot schema equivra.snapshot.v1 with canonical recursively key-sorted JSON payload SHA256; HTML/CSV use frozen payload only. Stable filenames from UUID; text/html;charset=utf-8 or text/csv;charset=utf-8 with attachment and nosniff. Export registerReportRoutes(app,deps:{db:Pool,data_dir:string}):Promise<void>; shared/report.ts exports renderHtml(snapshot:Snapshot):string and renderCsv(snapshot:Snapshot):string. Canonical payload hash uses shared/canonical.ts. Fixture snapshot.json is wire illustration only; full published cases required in actual payload.

**Preconditions**
C-DB run lock order and C-API expected versions; no immutable input/source missing; unresolved evidence is allowed but explicitly labeled in frozen output.

**Postconditions**
Saving is still draft; freezing pins exact review set; subsequent saves create a new reviewable version and never mutate snapshot. Repeated freeze same(run,review_version) returns stable snapshot; idempotency replay precedes stale checks.

**Error Semantics**
409 stale/incomplete/integrity;503 export failure; no partial snapshot. Unknown/ambiguous remains labeled after reviewer noted disposition; noted does not equal financial support.

**Idempotency Retry**
Repeat render has identical financial facts/evidence/decision text; metadata from snapshot, not current time/latest joins. Corrected complete bundle preserves original export facts.

**Ordering Concurrency**
Review and freeze take same run lock; save-before-freeze conflicts on old expected version; freeze-before-save fixes old snapshot and later save makes new draft. Database constraints/role protect history.

**Fixture**
Existing expected.json scenario; CREATE docs/contracts/examples/snapshot.json and report expectation examples; TASK-09 adds output/adversarial fixtures before consumer merge.

**Freeze Point**
Snapshot shape now; executable freeze after review/freeze concurrency, correction reproducibility and escaping conformance; no current artifact is application output.

**Verification**
HTML escapes untrusted text including attributes; CSV RFC4180 quoting plus prefix apostrophe for free text with formula prefix (=,+,-,@ after whitespace), preserving original raw source separately; typed numeric minor values rendered deliberately as numbers/decimal text. Test dangerous text at UI and actual download boundary, plus unchanged facts after correction.

**Lifecycle**
v1 is design-frozen after this plan review; executable freeze requires provider conformance and foundation evidence. No implicit backward-incompatible changes.

**Change Protocol**
Identify every consumer; update this record, examples, generated/typed interfaces, affected packets and edges; rerun conformance; re-sequence before merging a breaking change.

**Security**
Local synthetic demo only; protect application routes with current startup code, exact Host/Origin and owning-revision validation. Never expose secrets or local paths.
