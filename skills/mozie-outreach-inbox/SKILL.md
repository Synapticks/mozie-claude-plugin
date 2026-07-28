---
name: mozie-outreach-inbox
description: Draft, review, approve, send, and verify personalized creator email in Mozie, then triage and reply to campaign inbox threads. Use for first-touch email, bulk email, follow-ups, inbox review, or creator replies. Public self-serve outreach is email-only.
---

# Run email outreach and inbox

Move campaign email safely while preserving exact thread context and delivery truth.

## Boundary

- Use only the public Mozie MCP in the active workspace and team.
- This skill is email-only. Never automate Instagram DMs, WhatsApp, managed operations, provider events, or finance writes.
- Start with `mcpContext.current`. Never switch context implicitly.
- Prefer one `execute` call for pagination, polling, and verification. Use stable per-recipient, per-message-version idempotency keys.

## First touch

1. Run the readiness checks from the `mozie-prepare-creators` skill. Exclude opt-outs, duplicates, prior contact, invalid recipients, and open conflicting workflows. A missing human name is a warning, not an email blocker, when the campaign permits its neutral greeting fallback.
2. Re-read the creator, email, campaign, thread, template, and sending connection immediately before drafting.
3. Render the exact recipient, subject, body, greeting, and sender. Use verified greeting name, workspace display name, verified profile name, then the campaign-approved neutral fallback such as `there`; never use a handle as a first name. Do not require a phone, Instagram identity, or WhatsApp state for email. Do not add a campaign link unless the user or approved template explicitly requires it.
4. Create approval-gated drafts with the supported campaign outreach method. Read the returned `approvalRequests` record and present its exact recipient count, exclusions, representative personalized messages, and approval scope.
5. Stop for explicit approval. Approval binds the exact recipients and message version; any material edit requires fresh approval.
6. After approval, approve that exact request through `approvalRequests`; never synthesize approval. Poll workflow runs to a terminal state and re-read persisted thread messages.
7. Report provider or external message IDs when available. `queued` is not `sent`, and `sent` is not `delivered`.

## Inbox and replies

1. List threads and messages, paginating fully. Prioritize creator-replied threads awaiting the brand.
2. Classify each inbound as interested, question, rate or terms, decline, contact handoff, auto-reply, or ambiguous.
3. Draft from the complete creator and thread context. Preserve prior promises, terms, and channel history.
4. Show a compact review table. Obtain explicit approval immediately before sending.
5. Send in the existing canonical thread, poll to terminal state, and verify the persisted outbound message.

On ambiguous failure, reuse the same idempotency key and inspect authoritative state before retrying. Retry failed recipients only; never replay the whole batch.

## Report

Return counts for drafted, awaiting approval, sent, delivered when known, failed, replied, excluded, and still actionable, with exact remediation for every blocker.
