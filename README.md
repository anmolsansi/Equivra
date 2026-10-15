# Equivra

**Follow a payment difference from source evidence to a reviewed, reproducible workpaper.**

Equivra is a planned payments investigation workbench for reviewing differences across payment processor, bank and accounting records. It brings the supplied evidence into one review flow, explains what each finding supports, and preserves the facts behind a frozen report.

**Current stage: planning complete; application implementation has not started.** This repository contains the product specification, architecture, synthetic examples and a 53-ticket development guide. The capabilities below describe the approved build, not a running service.

## What we are building

A local web application where a reviewer can:

1. Import a complete bundle of three documented CSV sources: processor movements, bank activity and accounting activity.
2. Validate the files and preview their contents before accepting an investigation.
3. Follow a durable investigation run into source-linked findings.
4. Inspect exact amounts, references, dates and evidence limits.
5. Read **“What this evidence shows”** and **“Next evidence check”** for a finding.
6. Record a versioned reviewer disposition without changing the source facts.
7. Freeze the selected evidence and review versions into an immutable workpaper, then export HTML or CSV.

The first version uses synthetic data, one modeled client workspace, one processor account and USD. It is designed as a reproducible local demonstration, with business validation alongside development.

## Why build it?

A bank deposit, a processor movement and an accounting entry describe different parts of the same financial story. Refunds, dispute reversals, settlement timing and incomplete exports can make the relationship difficult to explain from a total alone.

Equivra focuses on the investigation: **which supplied records support this relationship, what differs, and what evidence is still needed?** The goal is to turn a selected discrepancy into a traceable review record rather than an unexplained spreadsheet adjustment.

The project also has a portfolio goal: demonstrate exact financial arithmetic, durable background processing, source lineage, safe retries, concurrent review and reproducible reports through one understandable user journey.

## Intended customers and users

The initial commercial hypothesis is **small bookkeeping firms reviewing payment activity for their clients**. This audience has not yet been validated through customer commitments or real-data pilots.

| Person | Their role in the proposed workflow | Intended benefit |
|---|---|---|
| Bookkeeper or reconciliation reviewer | Investigates processor, bank and accounting differences | Inspect related evidence and identify the next evidence check in one place |
| Firm owner or review lead | Reviews the investigation and its supporting workpaper | See what was supplied, what was concluded and what remains unresolved |
| Client or evidence provider | Supplies records or clarifies an unresolved reference | Receive a specific evidence request instead of an unsupported conclusion |
| Founder and portfolio viewer | Uses the initial local synthetic demonstration | Follow the financial story and observe correctness and recovery behavior |

These are modeled participants, not existing customers or separate V1 application accounts. The first application has one local reviewer workflow. Multi-user permissions, customer portals and hosted access require later decisions.

## Where Equivra fits in a customer's work

The proposed fit is an **investigation step within an existing reconciliation or period-close process**:

```text
Processor activity + bank records + accounting records
                         |
             A difference needs investigation
                         |
       Equivra: inspect evidence, review, freeze workpaper
                         |
       Reviewer carries the result into their existing
       accounting process or requests more evidence
```

The processor, bank and accounting system remain the sources of their records. Equivra preserves the supplied exports and the reasoning supported by them. Any accounting correction or financial action takes place separately in the customer's existing process.

V1 accepts files manually in the exact supported profiles. It does not synchronize live accounts, post journal entries or move money. Bookkeeping firms' source availability, recurring investigation needs and willingness to pay remain questions to validate.

## What problems will it address?

| Investigation problem | Planned Equivra behavior |
|---|---|
| Related evidence is spread across exports | Show original source values and stable file/row references alongside each finding |
| Equal amounts look like a match | Use explicit supported references; preserve ambiguity when identity is insufficient |
| A refund appears in processor data but not in supplied books | Show an incomplete-evidence case and the next evidence check; do not claim the real books are wrong |
| Settlement crosses a reporting boundary | Distinguish event, payout, bank and accounting dates and declared coverage |
| A repeated import or interrupted job risks duplicate results | Keep revision ownership and repeat-safe processing with visible recovery status |
| Two review actions use the same old version | Reject stale writes rather than overwrite a newer decision |
| Updated evidence changes a previously shared explanation | Create a new revision and preserve the original frozen workpaper |

The intended value is a clearer, repeatable investigation. Time saved, repeat use, accuracy improvements and commercial demand are **not measured outcomes yet**.
