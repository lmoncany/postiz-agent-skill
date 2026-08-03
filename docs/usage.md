# Postiz Agent usage

This repo packages a reusable Hermes skill plus documentation for scheduling posts through Postiz with either the CLI or the public API.

## Install

If the package is published, install it with:

```bash
npx skills add gitroomhq/postiz-agent
```

If you are working from a local checkout, copy the skill into your Hermes skills directory:

```bash
cp -R skills/mcp/postiz-agent ~/.hermes/skills/mcp/
```

## What it covers

- CLI scheduling with `postiz`
- API scheduling with integration IDs
- Verification of queued/published posts
- Multi-account and multi-workspace usage
- A documented, reusable workflow for Hermes sessions

## When to use Postiz

Use Postiz when you want Hermes to:

- publish on LinkedIn, X, Reddit, or another connected platform
- reuse the same workflow in a different workspace
- schedule posts that require explicit verification
- keep the integration selection human-readable and safe

## Human-in-the-loop rule

Postiz can automate the scheduling step, but the workflow should still be checked before claiming success:

1. confirm the connection
2. list integrations
3. schedule the post
4. verify the created post

## Repo layout

- `skills/mcp/postiz-agent/SKILL.md` — the reusable Hermes skill
- `skills/mcp/postiz-agent/references/postiz-public-api.md` — endpoint and CLI notes
- `assets/postiz-agent-banner.png` — README banner
