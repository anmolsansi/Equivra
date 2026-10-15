# C-API evidence guidance change — 2026-10-15

Status: approved planning addition; runtime not implemented.

User authorization: “ok add it then deploy the changes to github,” following the recommendation to add clear explanations and exactly what evidence is still needed.

Owner: architecture defines C-API UI copy; TASK-10 / T44 implements it in its existing App.tsx ownership and tests/e2e/workbench.test.ts suite. Protocol foundation TASK-01 and API assembly TASK-11 retain wire ownership unchanged. All C-API consumers retain the same fields, statuses, access and version semantics. No new dependencies, migration, fixture wire shape or DAG edges.

Inputs: existing facts.reason_code, evidence_state, amounts and source references. Outputs: two inert case-detail text labels, with exhaustive known-code mapping and safe unknown/absent fallback. Full copy, limits and test obligations are in architecture section 5 and every copied C-API record. Existing api-responses.json case_read supplies MISSING_BOOK_EVIDENCE; all-code controlled responses are created by T44 before acceptance, not claimed to exist today.

Freeze: documented copy is fixed for implementation; executable acceptance requires T44 mapping/fallback/security tests and T46 / INT-03 real-provider S1. Changes after freeze update the authoritative registry, architecture, every copied contract and affected tests/packets before handoff. Snapshot exports do not consume this UI copy.

Compatibility and rollback: additive presentation only; no amount, source, rule, review, API or stored snapshot change. Revert the UI lookup without modifying durable history. No new logs, external requests or automatic writes. Existing G0/provider/release gates remain mandatory. Prior runtime evidence: none.
