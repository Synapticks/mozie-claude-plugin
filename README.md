# Mozie Claude Plugin

Run creator campaigns through focused skills and the public Mozie MCP in your
authorized workspace.

## What it includes

- A remote MCP connection to `https://mcp.mozie.app`.
- Five skills for campaign launch, creator preparation, approval-gated email,
  deals and content, and campaign closeout.
- Public Mozie branding and documentation links.

This repository deliberately contains no Mozie server source code, credentials,
OAuth material, customer data, reviewer accounts, or internal operational
configuration.

Public self-serve outreach is email-only. The plugin excludes managed
operations, Instagram and WhatsApp automation, provider-event controls, admin
tools, and finance writes.

## Install and connect

After installing the plugin, open `/mcp` in Claude Code and complete the Mozie
OAuth sign-in flow. The plugin connects only to the workspace your Mozie account
is authorized to use.

In a local checkout, test the package with:

```sh
claude --plugin-dir .
```

Then use `/reload-plugins` after editing plugin configuration.

Claude can select a skill automatically from the request. To force a phase,
invoke `/mozie:mozie-launch-campaign`, `/mozie:mozie-prepare-creators`,
`/mozie:mozie-outreach-inbox`, `/mozie:mozie-deals-content`, or
`/mozie:mozie-close-campaign`.

## Example requests

- “Launch a campaign from this brief and build a verified shortlist.”
- “Prepare this roster and draft personalized email outreach.”
- “Review campaign health and recommend the next actions.”

## Privacy and support

Use Mozie only with data and workspaces you are authorized to access. External
outreach remains subject to explicit approval in the Mozie workflow.

- Documentation: [Mozie MCP docs](https://mozie.app/docs/mcp)
- Privacy: [Mozie Privacy Policy](https://mozie.app/legal/privacy)
- Terms: [Mozie Terms of Service](https://mozie.app/legal/terms)
- Support: [mozie.app](https://mozie.app) or `support@mozie.app`
