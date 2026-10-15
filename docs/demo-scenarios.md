# Equivra — synthetic demonstration scenarios

Status: scenario expectations for engineering design; no CSV fixtures or application code exists yet.
Authority: the approved design and decisions D8–D12. All identifiers, dates, and amounts below are invented. These examples are test inputs, not statements about universal processor fees or accounting treatment.

## S1 — Partial refund and missing accounting evidence

Supplied processor movements for the example automatic payout:

| Synthetic record | Gross USD | Supplied fee USD | Net USD | Reference |
|---|---:|---:|---:|---|
| Payment movement | 100.00 | 3.20 | 96.80 | ch_demo_01 |
| Partial-refund movement | -30.00 | 0.00 | -30.00 | re_demo_01, original ch_demo_01 |

The source explicitly assigns both movements to payout `po_demo_01`, whose supplied total is 66.80 USD. The synthetic bank export contains a single 66.80 USD deposit explicitly referencing that payout. The accounting export has the payment/fee evidence expected by its documented contract but no row referencing this refund in the declared export scope.

Expected: show the exact 66.80 bridge and supported processor-to-bank reference, plus a separate incomplete accounting-evidence case for the refund. Show source rows and declared export scope. Do not conclude that the real books are wrong or that the refund entry never existed. The zero supplied refund fee is a fixture fact, not a fee-refund policy.

## S2 — Dispute withdrawal followed by reversal

Supply separate identified movements for a 100.00 USD dispute withdrawal, a later 100.00 USD reversal, and any separately supplied fee row. Each event has its own timestamp, economic identity and source reference. The exact adapter categories/sign mapping must be documented before generating the fixture.

Expected: the principal movement across withdrawal/reversal sums to zero; both events remain visible. Only supplied fee movements affect the fee result. Do not invent a fee refund, count the reversal as a new sale, or call every dispute movement a permanent loss. If the later reversal is outside the declared evidence window, report the evidence limit rather than fabricate it.

## S3 — Payout crosses a period boundary

Supply payout membership in the September scope and a referenced bank deposit posting in October. Explicitly include adjacent-period bank evidence in the declared bundle scope.

Expected: distinguish processor event, payout/expected-arrival, bank posting and accounting dates. A cross-period date difference does not alone mean missing money. Support the relationship using the explicit reference and actual supplied amount; when adjacent evidence is omitted, keep the result unresolved/incomplete.

## S4 — Same amount is not identity

Supply two bank rows with different source IDs and the same amount, with no sufficient reference to select one for the payout. Both rows are valid separate transactions.

Expected: preserve both rows and show ambiguous evidence. Reordering the file cannot change the result to a supported first-row match. Content/amount deduplication must not delete a legitimate transaction.

## S5 — Invalid and incomplete sources

Exercise missing source kind, zero-byte CSV, invalid UTF-8, malformed quoting, missing required field, unsupported currency, invalid monetary precision, invalid date and cross-source account/scope conflict.

Expected: identify source and validation reason, with bounded diagnostics. Do not publish a partial completed run or silently round/coerce an invalid value. Header-only supported-source semantics must be explicit in the source contract; empty bytes are never equivalent to a valid declared empty scope.

## S6 — Repeat, correct, and interrupt

1. Import and process the accepted S1 bundle.
2. Repeat the same submission and retry processing around the commit boundary.
3. Freeze its reviewed workpaper.
4. Submit a complete corrected three-source bundle with the additional supported accounting evidence.
5. Allow an old worker to finish after the newer revision exists.

Expected: no repeated financial result; a new revision for changed evidence; old source/report facts unchanged; old job cannot publish into the new revision. The corrected run can change the accounting finding only according to its new evidence and documented rule, not by mutating the old case.

## S7 — Competing review and freeze

Pause two clients after they read the same review version. Submit both orders of review writes. Separately interleave a saved disposition with freezing the old displayed review set in both completion orders.

Expected: exactly one same-version review write succeeds; the other receives conflict. A stale freeze creates no snapshot. A freeze that commits before a later edit remains immutable, while that edit belongs to a new reviewable version. Do not use timed sleeps as the proof of ordering.

## S8 — Safe local access, output and capacity

Exercise missing/incorrect/previous-start access code, unapproved Host/origin, cross-revision IDs, source strings containing markup or spreadsheet-formula prefixes, and each accepted upload bound with one-over-bound examples.

Expected: unauthorized application access fails; strings remain inert in the UI/report; raw evidence remains intact and separate from safe export representation; each source file is limited by both 10,000 data rows and 10 MiB. Reject rather than truncate. Record actual duration/memory/hardware before making performance claims.

## Walkthrough sequence

Show S1 end to end: access, preview three sources, process, inspect supported bank evidence and incomplete book evidence, save a disposition, freeze and export. Use S4 to show honest ambiguity and S6–S7 to prove replay/recovery/version correctness. The viewer should see a working investigation story before any implementation internals are explained.

## Engineering handoff requirement

The source-contract owner must map these narratives into valid/invalid CSV fixtures and machine-checkable expected results. A consumer can rely on a scenario only after field/sign/date/lifecycle mappings and evidence scope are frozen. These narratives alone are not executable acceptance evidence, accounting advice, or a customer-data integration.
