# Mozie Claude Plugin

Find, evaluate, and run personalized creator campaigns in your authorized Mozie
workspace.

## What it includes

- A remote MCP connection to `https://mcp.mozie.app`.
- A workflow skill for creator discovery, campaign review, and approval-gated
  outreach.
- Public Mozie branding and documentation links.

This repository deliberately contains no Mozie server source code, credentials,
OAuth material, customer data, reviewer accounts, or internal operational
configuration.

## Install and connect

After installing the plugin, open `/mcp` in Claude Code and complete the Mozie
OAuth sign-in flow. The plugin connects only to the workspace your Mozie account
is authorized to use.

In a local checkout, test the package with:

```sh
claude --plugin-dir .
```

Then use `/reload-plugins` after editing plugin configuration.

## Example requests

- “Find creators for my campaign brief and explain the fit.”
- “Show my campaign health and the highest-priority next actions.”
- “Draft personalized outreach, then ask for approval before sending.”

## Privacy and support

Use Mozie only with data and workspaces you are authorized to access. External
outreach remains subject to explicit approval in the Mozie workflow.

- Documentation: [Mozie MCP docs](https://mozie.app/docs/mcp)
- Privacy: [Mozie Privacy Policy](https://mozie.app/legal/privacy)
- Terms: [Mozie Terms of Service](https://mozie.app/legal/terms)
- Support: [mozie.app](https://mozie.app) or `support@mozie.app`
