---
name: mozie-prepare-creators
description: Verify a Mozie campaign roster before outreach by resolving creator identity, duplicates, names, contact information, pricing, prior contact, and readiness. Use for roster cleanup, contact enrichment, personalization readiness, or pre-outreach review.
---

# Prepare Mozie creators

Produce a trustworthy, actionable roster. Do not send outreach.

## Guardrails

- Use only the connected public Mozie MCP in the active workspace and team.
- Never use managed-operations, admin, cross-tenant history, Instagram, WhatsApp, provider-event, or finance-write methods.
- Start with `mcpContext.current`. Use stable idempotency keys for enrichment or other writes and verify every write with a fresh read.
- Prefer one `execute` call for paginated reads and bounded workflow polling.

## Workflow

1. Read the campaign, its creator rows, existing threads, and current-workspace campaign history.
2. Resolve identity using stable platform identifiers. Treat handles as aliases, not durable identity.
3. Detect duplicate rows before enrichment or drafting. Never merge uncertain identities automatically.
4. Resolve personalization names with this precedence: verified greeting name, workspace display name, verified profile name. Never derive a first name from a handle or brand-like display name.
5. Resolve contacts with this precedence: verified manual/operator value, then fetched or enriched value. Never overwrite a valid manual contact with enrichment.
6. Enrich only missing information. Poll returned workflows to a terminal state, then re-read the creator rows.
7. Check authorized prior outreach, opt-outs, existing campaign membership, live threads, proposals, contracts, deals, and available pricing.
8. Classify every row as one of: `ready`, `prior_contact`, `missing_email`, `invalid_email`, `uncertain_name`, `duplicate`, `opt_out`, `open_deal`, or `error`.

## Review output

Return a compact table with creator, resolved identity, greeting, email readiness, prior-contact state, pricing state, classification, and exact next action. Separate uncertain rows from the send-ready set. Hand send-ready rows to the `mozie-outreach-inbox` skill.
