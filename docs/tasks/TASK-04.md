# TASK-04 — Enforce current-start local access and browser boundary

Status: future implementation packet. Coding authorization and G0/provider gates are not passed. TASK-01 owns bootstrap/G0 and may start only after coding authorization; downstream packets wait the declared handoffs. No done claim.

**Objective**
Enforce current-start local access and browser boundary.

**Why this task exists**
Own the approved Access outcome without weakening money/evidence/version/access/recovery guarantees. No extra product scope.

**Workstream / execution wave**
Access, W1 (start wave, not merge permission).

**Depends on**
- TASK-01 via C-FOUNDATION,C-API; start=G0 + design-frozen shapes and fixtures; merge=Provider executable conformance for C-FOUNDATION,C-API

**Blocks / consumers**
- TASK-05 via C-ACCESS
- TASK-07 via C-ACCESS
- TASK-08 via C-ACCESS
- TASK-09 via C-ACCESS
- TASK-10 via C-ACCESS
- TASK-11 via C-ACCESS
- TASK-12 via C-ACCESS
- INT-02 via INT-02

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
- CREATE server/access.ts
- CREATE server/app.ts
- CREATE tests/unit/access.test.ts
- CREATE tests/integration/access.test.ts

**Non-owned / do-not-touch files**
All files outside the owned list.
- package.json — another packet or architect owns it; no casual contract edits.
- package-lock.json — another packet or architect owns it; no casual contract edits.
- db/001_initial.sql — another packet or architect owns it; no casual contract edits.
- server/worker.ts — another packet or architect owns it; no casual contract edits.
- web/src/App.tsx — another packet or architect owns it; no casual contract edits.
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
C-FOUNDATION, C-API

**Contracts produced**
C-ACCESS

**Implementation steps**
1. Generate per-start code with crypto and bounded constant-time Bearer comparison. Intentional terminal display only, structured logs redacted.
2. Install protected /api/v1/download guard globally; shell/minimal health reveal no app data.
3. Enforce loopback/exact Host/mutating Origin/cross-site checks and declared bounded failed-code throttle. Use normal Fastify plugin/config wiring, no test bypass.

**Invariants affected**
- INV-01: Only the current-start code may access application data/actions; loopback/Host/Origin enforced; worker cannot insert reviewer decisions/snapshots.
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
- Current code allowed; missing/wrong/previous-start401; hostile Host/Origin/null/cross-site403 even with code.
- Content/size checks reject before handler; failed-code threshold429.
- Captured JSON/errors/structured logs/URLs do not contain code; browser memory/reload assertions at INT-03.
- Regression: retain every relevant S1-S8 accepted money/uncertainty/replay/correction/review/report/access bound; no old tests exist to retire.

**Verification commands**
Current repository application commands: NONE verified. Host versions were inspected but do not prove Node24. After TASK-01 G0, exact proposed scripts are npm run typecheck, npm run build, npm run test:unit, npm run test:integration, npm run test:e2e, npm run db:migrate as applicable under pinned Node24 local environment. They are specifications until created/inspected/invoked and recorded in repo_context. Missing/failed/zero-test suite is not acceptance. Run the behavior-specific families listed above; do not broaden unrelated suites without cause.

**Acceptance criteria**
1. PASS/FAIL: All data/actions/downloads guarded before domain work.
2. PASS/FAIL: Restart revokes old access, health/static cannot disclose it.
3. PASS/FAIL: Safe error mapping and no writes on denied request.

**Rollback / recovery**
Stop local API to revoke code; keep data intact; never fallback to an unguarded mode.

**Downstream handoff**
Give consumer the frozen shape/examples/error/version/ownership semantics copied below plus actual provider conformance. It must not need provider-private code. Mark every unverified contract not-yet-consumable and block merge. Runtime-only packets hand off checkpoint evidence without changing the protocol.

**Definition of done**
All owned code/tests/docs/config complete; all numbered criteria and applicable verified commands pass; produced contracts executable-frozen or explicitly blocked; no hidden design choice assigned to builder; unrelated files untouched. This packet is not currently implemented.

**Effort**
0.75 engineer days at8h/day, preliminary sizing <=3-day cap; main cost is behavior/integration verification. TASK-01 is an atomic bootstrap exception to the usual small file count: splitting required runtime/type/mock configuration into file-only tickets would not yield independent outcomes. Calendar pace is10h/week; no measured AI speedup or completion promise.

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
