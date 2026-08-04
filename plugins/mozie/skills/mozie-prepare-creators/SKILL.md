---
name: mozie-prepare-creators
description: Verify a Mozie campaign roster before outreach: creator identity, duplicates, names, contacts, and pricing. Use for roster cleanup, enrichment, or pre-outreach readiness checks.
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
4. Resolve personalization names with this precedence: verified greeting name, workspace display name, verified profile name. Never derive a first name from a handle or brand-like display name. If no trustworthy human name exists, use the campaign-approved neutral greeting such as `there` and report a warning; do not block email unless the campaign explicitly requires a human name.
5. Resolve contacts with this precedence: verified manual/operator value, then fetched or enriched value. Never overwrite a valid manual contact with enrichment.
6. Enrich only missing information. Poll returned workflows to a terminal state, then re-read the creator rows.
7. Check authorized prior outreach, opt-outs, existing campaign membership, live threads, proposals, contracts, deals, and available pricing. Apply channel-specific readiness: email requires a valid email and active email sender, never a phone, Instagram identity, or WhatsApp state.
8. Treat public server-returned outreach blockers as authoritative. Do not claim or reconstruct internal cross-tenant Ops preflight. Classify every row as one of: `ready`, `name_fallback`, `prior_contact`, `missing_email`, `invalid_email`, `duplicate`, `opt_out`, `open_deal`, or `error`.

## Review output

Return a compact table with creator, resolved identity, greeting, email readiness, prior-contact state, pricing state, classification, and exact next action. Keep `name_fallback` rows send-ready but visibly warned. Hand send-ready rows to the `mozie-outreach-inbox` skill.
