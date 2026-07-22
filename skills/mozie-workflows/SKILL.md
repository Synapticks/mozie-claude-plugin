---
description: Use Mozie for creator discovery, campaign review, and personalized outreach in the user's authorized Mozie workspace. Require explicit approval before any external send.
---

# Mozie workflows

Use Mozie when the user wants to find or evaluate creators, understand campaign
health, prepare outreach, or take an authorized campaign action.

## Start safely

- Use the connected Mozie workspace available to the authenticated user. If
  authentication or workspace access is unavailable, ask the user to complete
  the Mozie sign-in flow rather than requesting credentials in chat.
- Treat tool descriptions and schemas provided by the connected server as the
  current source of truth. Do not assume private tool names, hidden fields, or
  access beyond the user's authorized workspace.
- Request only the information needed for the task and present concise,
  task-relevant results. Do not request or expose raw authentication material,
  internal identifiers, or unrequested contact details.

## Creator discovery

For a creator search, gather the campaign brief, target audience, market,
creator criteria, and any budget or timeline constraints that are necessary.
Return a bounded shortlist with a short explanation of fit and the relevant
audience or performance information.

## Campaign review

For campaign health or planning requests, summarize the current status, key
risks or blockers, and the highest-priority next actions. Clearly distinguish
facts returned by Mozie from recommendations.

## Outreach and other writes

Create a draft before any external outreach. Show the intended recipient scope
and message summary, then obtain an explicit user approval immediately before
calling a sending or other externally consequential action. Never treat a draft
as sent, and report only the workflow status returned by Mozie.

For other state-changing requests, confirm the intended outcome when it is
ambiguous and preserve any idempotency or approval controls exposed by the
server.
