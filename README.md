# Living Memory for Grok Build

![Living Memory](logo.png)

A shared place to return to. Connect Grok Build to your hosted Living Memory World to save memories, recall earlier context, and leave temporary handoffs for another agent.

This is the hosted integration. It is different from the Local stdio plugin: canonical memory is held by the Living Memory service, not on this device.

## Install

```sh
grok plugin install Nature-Labs-Orz/living-memory-grok-plugin
```

Complete the Living Memory OAuth sign-in when Grok requests it. Sign in with your own account; the connection uses your existing World. If you do not yet have an accessible World, follow Living Memory's onboarding. The plugin does not grant free storage or bypass account entitlement. Signing in does not itself buy a plan; manage availability and billing through the Living Memory website.

After installation, start a new Grok session. Open `/mcps`, select `living-memory`, and press `i` to authenticate. If the server list has not refreshed, press `r`. Grok account login and Living Memory authorization are separate connections.

Once connected, try:

- "Which Living Memory World am I connected to?"
- "Remember in Living Memory that I prefer concise weekly project updates."
- "What project launch decision did I save in Living Memory?"
- "Leave a Living Memory handoff labelled next-agent: Check the launch checklist. Keep it for one hour."
- "List my Living Memory handoffs and read next-agent."

## What is included

- `.grok-plugin/plugin.json`: plugin metadata.
- `.mcp.json`: one remote HTTP MCP connection to `https://lme.viibe.to/mcp`.
- `skills/living-memory/SKILL.md`: guidance for explicit writes, grounded recall, temporary handoffs, and truthful error reporting.

There are no lifecycle hooks, executable setup scripts, bundled credentials, or local shell MCP tools. Available tools are supplied by the authenticated server and may depend on the connection's permissions.

## Authentication, network, and data

Grok communicates with the hosted MCP endpoint `https://lme.viibe.to/mcp`. Its OAuth flow uses Living Memory's published authorization discovery, sign-in at `https://viibe.to/living-memory/oauth/login/`, and the authentication provider presented during sign-in. No API key or password is embedded in this repository. Let the host manage the OAuth connection; never paste credentials into a chat or commit them to configuration.

Memory text is stored in your hosted World. The service sends memory/search text to its configured external embedding provider for semantic retrieval; this is not an offline integration. Handoff notes are temporary, are not embedded, and expire after their requested lifetime (24 hours by default, maximum 72 hours). Posting a handoff may deliver it to configured external event subscribers. Reading a live note does not consume it; handoff operations can permanently remove expired notes. Forgetting memories is permanent.

The plugin has no additional telemetry scripts. The hosted service's data handling and account terms are described in the linked policies. Do not store passwords, one-time codes, tokens, or other authentication secrets.

If a tool fails, Grok should report the failure rather than claim a successful write or an empty World. A temporary handoff is not a durable-memory substitute. This package does not claim native Grok MCP Events subscription support.

## Help and policies

- [Website](https://viibe.to/living-memory)
- [Documentation](https://getsquish.gitbook.io/living-memory/)
- [Support](https://viibe.to/living-memory/support/)
- [Privacy](https://viibe.to/living-memory/privacy/)
- [Terms](https://viibe.to/living-memory/terms/)

## License

Apache-2.0 applies to this integration package. The hosted service is governed by its own terms; this package's license does not license the hosted backend or users' memories. Maintained by Nature Labs.
