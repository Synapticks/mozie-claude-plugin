---
name: mozie-launch-campaign
description: Create or reuse a Mozie campaign, turn a brief into discovery constraints, find and review creators, and build a verified shortlist. Use for new campaign setup, creator discovery, ICP-led searches, collections, or adding selected creators to a campaign.
---

# Launch a Mozie campaign

Build the smallest accurate campaign and shortlist that satisfies the user's brief. Stop before outreach.

## Guardrails

- Use only the connected public Mozie MCP and the user's active workspace and team.
- Never use managed-operations, admin, Instagram, WhatsApp, provider-event, or finance-write methods.
- Begin with `mcpContext.current`. Never infer a workspace or switch context unless the user requests an authorized switch.
- Prefer one `execute` call that performs pagination and polling internally. Use `search_docs` only when the current SDK shape is unclear.
- Give every mutation a stable `Idempotency-Key` through request options. Re-read mutated resources before reporting success.

## Workflow

1. Parse the brief into hard constraints and ranking preferences. Ask one consolidated question only when a missing goal, audience, platform, geography, budget, or timeline would materially change the result.
2. List current campaigns. Reuse an exact or clearly intended campaign; do not create a duplicate. Otherwise create one with the normalized brief.
3. Choose discovery deliberately:
   - Use `creators.briefSearch` for a fast, synchronous pool.
   - Use `discoverySearches.create` for multi-constraint or reasoned scoring.
4. For an asynchronous search, poll its durable ID to a terminal state. If it reaches `awaiting_review`, inspect the questions and call `discoverySearches.proceed` once with consolidated clarifications and the same idempotency key.
5. Read compact result summaries. Apply hard constraints first, then rank by fit. Explain material exclusions instead of silently relaxing the brief.
6. Show a bounded review table with creator, platform, fit, evidence, important metrics, and risk. Do not treat directory metrics as canonical campaign metrics.
7. Persist only the selected results. Create or reuse a collection when the user wants an intermediate review set; add creators to the campaign only after selection is clear.
8. Re-list the campaign roster and verify the resulting creator IDs and count.

If a search outlives the session, return its durable search ID and current status. Resume that search later rather than creating another.

## Handoff

Return the campaign, normalized constraints, selected creators, exclusions, unresolved risks, and the next recommended step. Use the `mozie-prepare-creators` skill before any outreach.
