# Resend Plugin for Grok

Use Resend in [Grok Build](https://github.com/xai-org/plugin-marketplace) to send transactional and marketing email, receive inbound email, build React Email templates, manage domains and templates, inspect delivery events, and follow deliverability best practices.

This plugin is skill-only. It does not bundle an MCP server, which avoids name collisions and authentication issues — the skills work through the Resend SDK, CLI, and API using `RESEND_API_KEY`.

## Included skills

- `resend` — the Resend email API: sending (single and batch), receiving via webhooks, templates, domains, contacts, broadcasts, webhooks, API keys, logs, automations, and events
- `agent-email-inbox` — secure inbound email workflows for AI agents: webhook setup, sender allowlists, content filtering, and safe processing of untrusted email
- `resend-cli` — operate Resend from the terminal, scripts, and CI/CD with the `resend` CLI
- `react-email` — build HTML email templates with React components, render them, and send with Resend
- `email-best-practices` — deliverability (SPF/DKIM/DMARC), compliance (CAN-SPAM, GDPR, CASL), retries, list management, and transactional vs marketing decisions

## Installation

Install from this repo's URL:

```
/install-plugin https://github.com/resend/grok-plugin
```

Once listed in the [xAI plugin marketplace](https://github.com/xai-org/plugin-marketplace), it will also be installable by name:

```
/install-plugin resend
```

## Setup

Bundled skills are available after install. For live API calls, set your API key in the environment where Grok runs:

```bash
export RESEND_API_KEY=re_xxxxxxxxxxxxxxxxx
```

Get your key at [resend.com/api-keys](https://resend.com/api-keys). Grok uses it through the Resend SDK, CLI, or API — no additional server needs to start.

## Plugin structure

- `.grok-plugin/plugin.json` — plugin manifest with metadata
- `skills/` — the bundled Resend skill set, auto-discovered by Grok
- `assets/` — plugin icon
- `marketplace-entry.json` — draft catalog entry for submission to the xAI plugin marketplace

## Notes

- The skills can still help with planning and code review when `RESEND_API_KEY` is not set.
- Sending, receiving, template management, and other live Resend API actions require `RESEND_API_KEY`.

## Submitting to the xAI plugin marketplace

After this repo is pushed to GitHub:

1. Get the commit SHA to pin (must be the full 40-character lowercase SHA — the marketplace validator rejects tags and short SHAs):
   ```bash
   git ls-remote https://github.com/resend/grok-plugin.git HEAD
   ```
2. Fork [xai-org/plugin-marketplace](https://github.com/xai-org/plugin-marketplace) and append the contents of `marketplace-entry.json` (with the real `sha`) to the `plugins` array in `.grok-plugin/marketplace.json`.
3. Regenerate the component index and validate:
   ```bash
   python3 scripts/generate-plugin-index.py
   python3 scripts/validate-catalog.py
   ```
4. Open a PR. CI runs the validator and code-owner review is required.
