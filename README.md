# Eventdoor for Claude

Run your Eventdoor live-event streaming site from Claude. This plugin does two things in one install:

- **Connects the Eventdoor MCP server**, so Claude can read and change your organizations, hubs, broadcasts, site pages, theme, collections, replays, products and paywalls as you, with only the access you have in the Eventdoor admin.
- **Adds the Eventdoor skill**, which teaches Claude how Eventdoor is organized, which changes are drafts and which are saved at once, what your organization's assistant settings allow, and step-by-step recipes for common jobs such as planning a season schedule, building a site from a brand, or finding out why a broadcast has no replay.

AI assistant access is in beta. To report a problem or share feedback, email support@eventdoor.com.

## Install

### Claude (web and desktop)

1. Open **Customize**, then **Plugins**.
2. Choose **Add**, then **Add marketplace**, and enter `eventdoor-hq/claude-plugin`.
3. Install **eventdoor**.
4. On the plugin's **Connectors** tab, add the **Eventdoor** connector. Under **OAuth client**, choose **Use your own OAuth client**, enter the client ID `eventdoor-assistant`, and leave the client secret blank.
5. Sign in with your Eventdoor account.

### Claude Code

```bash
claude plugin marketplace add eventdoor-hq/claude-plugin
claude plugin install eventdoor@eventdoor
```

Then run `/mcp`, choose the Eventdoor server, and choose **Authenticate** to sign in.

## Documentation

Setup, what an assistant can do, and troubleshooting: [docs.eventdoor.com/ai-assistants](https://docs.eventdoor.com/ai-assistants).

## About this repository

This repository is published from Eventdoor's source and is updated with each release. Changes made here directly are overwritten; please send issues and suggestions to support@eventdoor.com.
