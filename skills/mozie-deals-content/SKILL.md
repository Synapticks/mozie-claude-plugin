---
name: mozie-deals-content
description: Negotiate creator terms and manage Mozie proposals, contracts, deliverables, reviews, revisions, publishing readiness, and tracking. Use after a creator responds or when advancing active campaign work.
---

# Manage deals and content

Advance each creator through commercial and content stages without duplicating records or overstating status.

## Guardrails

- Use only the public Mozie MCP in the active workspace and team.
- Start with `mcpContext.current`. Use stable idempotency keys for mutations and re-read each resource after a write.
- Never use managed-operations, admin, Instagram, WhatsApp, provider-event, or finance-write methods.
- Treat externally consequential sends and approvals as approval-gated.

## Terms and agreements

1. Read the existing thread, deal, proposal, contract, and deliverables before creating anything. Reuse or supersede; never create a parallel record accidentally.
2. Keep the creator's rate card, brand offer, creator counter, accepted proposal, and signed contract as distinct facts.
3. Normalize currency, deliverables, quantities, unit prices, usage rights, exclusivity, whitelisting, revisions, dates, and payment terms.
4. Ask for explicit authorization before accepting, declining, countering, or sending an agreement.
5. For proposal or contract sends, poll the workflow to terminal state and re-read recipient status and safe links. Never infer acceptance or signature from a message.

## Content

1. Read the expected deliverables and current submission lineage.
2. Preserve every asset, revision request, decision, and resubmission as structured history.
3. Approve or request revisions only against the intended current submission.
4. Keep content approval distinct from publication. Use a supported publishing path only when it exists; otherwise report the capability gap.
5. Create or verify tracking links before go-live when the campaign requires them.

## Report

Return one row per creator with negotiation stage, agreed terms, proposal and contract status, deliverable state, next owner, due date, and blocker. Do not perform charges, payouts, or settlement.
