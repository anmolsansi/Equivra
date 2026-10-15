# TASK-06 — Investigate supported and unresolved financial evidence deterministically

Status: future implementation packet. Coding authorization and G0/provider gates are not passed. TASK-01 owns bootstrap/G0 and may start only after coding authorization; downstream packets wait the declared handoffs. No done claim.

**Objective**
Investigate supported and unresolved financial evidence deterministically.

**Why this task exists**
Own the approved Domain outcome without weakening money/evidence/version/access/recovery guarantees. No extra product scope.

**Workstream / execution wave**
Domain, W2 (start wave, not merge permission).

**Depends on**
- TASK-01 via C-FOUNDATION; start=G0 + design-frozen shapes and fixtures; merge=Provider executable conformance for C-FOUNDATION
- TASK-02 via C-SOURCE; start=G0 + design-frozen shapes and fixtures; merge=Provider executable conformance for C-SOURCE

**Blocks / consumers**
- TASK-07 via C-DOMAIN
- TASK-09 via C-DOMAIN
- TASK-11 via C-DOMAIN
- TASK-12 via C-DOMAIN
- INT-01 via INT-01

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
- CREATE shared/investigate.ts
- CREATE tests/unit/investigate.test.ts

**Non-owned / do-not-touch files**
All files outside the owned list.
- package.json — another packet or architect owns it; no casual contract edits.
- package-lock.json — another packet or architect owns it; no casual contract edits.
- db/001_initial.sql — another packet or architect owns it; no casual contract edits.
- server/app.ts — another packet or architect owns it; no casual contract edits.
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
C-FOUNDATION, C-SOURCE

**Contracts produced**
C-DOMAIN

**Implementation steps**
1. Implement seven frozen C-DOMAIN rules using bounded indexed maps and exact integers, no I/O or model.
2. Stable case keys/order and references; amount alone never identity. Keep missing/ambiguous/unsupported separate from computation errors.
3. Preserve scope/date/refund/dispute limits and unlinked observations; no invented fees, wins, losses or accounting advice.

**Invariants affected**
- INV-02: All monetary arithmetic uses exact integer cents, currency usd, source values preserved; gross-fee=net verified; no guessed fees.
- INV-04: Source event identities remain distinct; duplicate submission/recovery creates one owning financial result; corrections and stale jobs cannot overwrite other revisions.
- INV-07: Incomplete/ambiguous/unsupported evidence remains explicit; a reviewer disposition or balanced supplied subtotal cannot prove complete real books.

**Failure/error semantics**
Apply exact named errors in copied contracts: invalid input422/400/413, access401/403/429, missing404, stale/replay/integrity409, dependencies503, unexpected500 safe correlation. Known uncertainty is an evidence state, not an empty success. Roll back rejected writes; never silently coerce money, truncate sources, overwrite history or complete failed jobs.

**Security/privacy**
Synthetic-only. Parameterized SQL, generated storage identifiers, owning-revision links, source text escaped, startup code/raw financial text redacted. Current access/Origin/Host before browser mutation. Worker cannot invent reviewer decisions or move money.

**Observability**
Runtime owner emits operation/correlation/bundle/run/job/snapshot IDs, outcome/error/attempt/duration with no raw text/secrets. Pure source/domain functions return typed diagnostics; caller logs once. No new monitoring vendor.

**Migration/backfill/compatibility**
TASK-03 owns initial schema. Others consume its constraints unchanged. No real-data backfill. V1 source/rule/API/snapshot changes follow architect change protocol and update all fixtures/consumers. Preserve immutable history; coordinated compatible rollback only.

**Required tests**
- S1 subtotal6680/missing book refund/corrected delta0; missing observed/delta is null, not zero.
- S2 exact same dispute identity only, principal and supplied fees distinct; S3 cross-period evidence; S4 reversed source order remains ambiguous.
- Unknown categories and extra/unlinked rows explicit; equal amounts/different IDs preserved; all facts resolve to source or exact calculation.
- Regression: retain every relevant S1-S8 accepted money/uncertainty/replay/correction/review/report/access bound; no old tests exist to retire.

**Verification commands**
Current repository application commands: NONE verified. Host versions were inspected but do not prove Node24. After TASK-01 G0, exact proposed scripts are npm run typecheck, npm run build, npm run test:unit, npm run test:integration, npm run test:e2e, npm run db:migrate as applicable under pinned Node24 local environment. They are specifications until created/inspected/invoked and recorded in repo_context. Missing/failed/zero-test suite is not acceptance. Run the behavior-specific families listed above; do not broaden unrelated suites without cause.

**Acceptance criteria**
1. PASS/FAIL: All normalized scenario facts match expected outcomes with evidence refs.
2. PASS/FAIL: Same input/rule yields deterministic financial facts and case keys.
3. PASS/FAIL: No uncertainty becomes supported because of amount equality or reviewer disposition.
4. PASS/FAIL: Worker/report consumers implement from published shape/fixture only.

**Rollback / recovery**
Changed rules need new rule/run version and consumer fixtures; never mutate historical output.

**Downstream handoff**
Give consumer the frozen shape/examples/error/version/ownership semantics copied below plus actual provider conformance. It must not need provider-private code. Mark every unverified contract not-yet-consumable and block merge. Runtime-only packets hand off checkpoint evidence without changing the protocol.

**Definition of done**
All owned code/tests/docs/config complete; all numbered criteria and applicable verified commands pass; produced contracts executable-frozen or explicitly blocked; no hidden design choice assigned to builder; unrelated files untouched. This packet is not currently implemented.

**Effort**
2 engineer days at8h/day, preliminary sizing <=3-day cap; main cost is behavior/integration verification. TASK-01 is an atomic bootstrap exception to the usual small file count: splitting required runtime/type/mock configuration into file-only tickets would not yield independent outcomes. Calendar pace is10h/week; no measured AI speedup or completion promise.

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

### C-DOMAIN — Deterministic evidence investigation

**Provider Component**
Financial domain

**Provider Task**
TASK-06

**Consumers**
TASK-07, TASK-09, TASK-11, TASK-12

**Type**
function/schema

**Source Of Truth**
docs/architecture.md section9; docs/demo-scenarios.md; CREATE shared/investigate.ts

**Inputs**
NormalizedBundle={manifest,sources:{stripe:ParsedSource,bank:ParsedSource,books:ParsedSource}}. Exact refs only. Rule version equivra.rules.v1.
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



**Outputs**
Investigation={rule_version,coverage:{basis:supplied_scope_only,observed_rows:{stripe,bank,books},warnings:[code]},summary:{cases_total,supported,difference,incomplete,ambiguous,unsupported},cases:[{case_key,kind,evidence_state,facts,evidence}]}. facts={currency:usd,expected_minor:string|null,observed_minor:string|null,delta_minor:string|null,reason_code:string,references:map of allowed payout_id,balance_transaction_id,charge_id,dispute_id}. Evidence={source_kind,row_no,source_sha256}. evidence_state supports five values including difference; exact taxonomy, delta/null and lifecycle rules pasted above are binding. Export investigate(bundle:NormalizedBundle):Investigation. Domain functions have no I/O; persistent case UUID/run/version are added only by worker publication.

**Preconditions**
Validated pinned normalized source bundle; no floats, DB, HTTP, filesystem or model.

**Postconditions**
Bank uses exact payout_ref and exactly one candidate+amount/currency; 0=incomplete,>1=ambiguous, unequal=difference. Books sums exact processor_ref lines for each balance event; missing=no observed/delta amount. Unknown categories=unsupported, same amount alone never supports. All unlinked observations explicit. Sort case_key and evidence deterministically; no duplicate economic allocation.

**Error Semantics**
Domain schema/invariant error fails run, not empty success; known incomplete/ambiguous/unsupported are case states, not exceptions. Never infer permanent loss or invent fee refunds/dispute identity.

**Idempotency Retry**
Same input+rule yields same case keys/facts/evidence. Case UUIDs are persistence identities, not arbitrary matching decisions.

**Ordering Concurrency**
Keys: payout:<payout_id>:bank; event:<balance_transaction_id>:books; event:<balance_transaction_id>:unsupported; bank:<bank_row_id>:unlinked; books:<entry_id>:unlinked; charge:<charge_id>:refunds; dispute:<source_id>:lifecycle only with explicit same dispute identity. No dependence on source order except evidence row locations.

**Fixture**
docs/contracts/examples/expected.json and docs/demo-scenarios.md; TASK-02 supplies normalized S2-S8 fixtures before final conformance.

**Freeze Point**
Shape frozen now; executable freeze after TASK-06 proves every supported rule and uncertainty case against source fixtures.

**Verification**
Unit fixture/properties: S1 subtotal6680 and missing refund, corrected books delta0, S2 principal reversal without invented fee, S3 dates, S4 reordered equal amounts; all gross/fee/net integer strings. Planned test:unit after G0.

**Lifecycle**
v1 is design-frozen after this plan review; executable freeze requires provider conformance and foundation evidence. No implicit backward-incompatible changes.

**Change Protocol**
Identify every consumer; update this record, examples, generated/typed interfaces, affected packets and edges; rerun conformance; re-sequence before merging a breaking change.

**Security**
Local synthetic demo only; protect application routes with current startup code, exact Host/Origin and owning-revision validation. Never expose secrets or local paths.
