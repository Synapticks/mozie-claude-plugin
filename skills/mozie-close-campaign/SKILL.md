---
name: mozie-close-campaign
description: Reconcile Mozie campaign health, outcomes, deliverables, tracking, invoices, payment obligations, and remaining actions before closeout. Use for reporting, campaign audits, ROI summaries, or safe completion.
---

# Close a Mozie campaign

Produce an evidence-backed closeout and change campaign status only when completion is real.

## Guardrails

- Use only the public Mozie MCP in the active workspace and team.
- Start with `mcpContext.current`. Prefer a single `execute` call that paginates all relevant resources.
- Finance is read-only in public self-serve. Never charge, pay, settle, approve payouts, or use managed-operations or admin methods.
- Use stable idempotency keys for any authorized status mutation and verify it with a fresh read.

## Workflow

1. Read the campaign, roster, threads, deals, proposals, contracts, deliverables, submissions, reviews, tracking links, performance, invoices, payment obligations, payments, and workflow runs that belong to it.
2. Separate `proposed`, `contracted`, `accrued`, `invoiced`, `paid`, `refunded`, and `failed`; never collapse them into one spend number.
3. Check freshness and contradictions: missing signatures, overdue content, approved-but-unpublished work, broken tracking, unresolved replies, failed workflows, and payment mismatches.
4. Summarize reach, responses, contracted creators, content status, attributable performance, committed spend, paid spend, and unresolved exposure.
5. Mark the campaign complete only when the evidence satisfies its closeout criteria and the user explicitly approves the status change.
6. Re-read the campaign after any update.

## Report

Return a compact executive summary, creator-level exceptions, financial reconciliation, data-freshness note, and a prioritized remaining-action list. State clearly when the public MCP cannot perform a required finance action.
