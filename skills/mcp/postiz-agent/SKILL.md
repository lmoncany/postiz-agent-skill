---
name: postiz-agent
description: "Use when scheduling, verifying, or managing social posts through Postiz CLI/API/MCP, especially across different integrations, accounts, or workspaces."
version: 1.0.0
author: Hermes Agent
license: MIT
metadata:
  hermes:
    tags: [postiz, mcp, cli, social-media, scheduling, automation]
    related_skills: [linkedin-content-pipeline, social]
---

# Postiz Agent

## Overview

Use this skill when you need to schedule or verify posts through Postiz from Hermes, especially when the job must work across different integrations, accounts, or workspaces.

The key rule is simple: **never hard-code an account**. Always discover integrations first, pick the one you want by `identifier`, then create and verify the post from the returned IDs.

## When to Use

- Schedule a LinkedIn, X, Reddit, or other supported social post through Postiz
- Verify whether a post is actually queued or published
- Switch between multiple connected accounts in the same Postiz workspace
- Reuse the same workflow in a different workspace with a different API key
- Document Postiz setup, CLI usage, or API usage for the current project

## Core Workflow

### 1) Check connection

Use the API or CLI to confirm Postiz is reachable before doing anything else.

- API: `GET /api/public/v1/is-connected`
- CLI: run the matching `postiz` connectivity command if installed in the environment

If this fails, stop and fix auth before scheduling.

### 2) List integrations

Discover the available integrations every time.

- CLI: `postiz integrations:list`
- API: `GET /api/public/v1/integrations`

Pick the target by `identifier`, not by a remembered ID.

Common identifiers include:
- `linkedin`
- `x`
- `reddit`
- `instagram`
- `youtube`
- `facebook`
- `threads`

### 3) Create the post

Prefer the CLI when it is available and readable. Use the API when you need explicit verification or when the CLI is missing.

CLI example:

```bash
postiz posts:create   -c "Post text"   -s "2026-08-04T09:00:00Z"   -i "<integration-id>"
```

API example:

```json
{
  "type": "schedule",
  "shortLink": false,
  "date": "2026-08-04T09:00:00Z",
  "tags": [],
  "posts": [
    {
      "integration": {"id": "<integration-id>"},
      "value": [
        {
          "content": "Post text",
          "image": [
            {"id": "<media-id>", "path": "https://..."}
          ]
        }
      ]
    }
  ]
}
```

### 4) Verify the result

Never trust the create response alone.

- API: `GET /api/public/posts/<id>`
- Confirm the returned `state`, publish/scheduled time, integration, and content
- If the post includes media, verify the media object is attached in the readback

### 5) Handle multiple accounts or workspaces

- **Same workspace, multiple accounts:** choose the right integration ID from the integration list
- **Different workspace/account:** use the other workspace’s API key or CLI auth context
- **Do not** reuse IDs from a different workspace unless you have confirmed they exist in the current one

## Common Pitfalls

1. **Hard-coding integration IDs.** These are workspace-specific. Always discover them first.
2. **Assuming the create response means success.** Always read back the post.
3. **Passing bare image URLs where Postiz expects media objects.** Upload first, then attach the returned media object.
4. **Forgetting that a different account may mean a different workspace.** A new account may need a new API key.
5. **Skipping the human check.** Postiz can automate the send, but a human still owns the final judgment.

## Verification Checklist

- [ ] Postiz connection check passed
- [ ] Integrations listed successfully
- [ ] Target integration selected by `identifier`
- [ ] Post created with CLI or API
- [ ] Post read back from the API and state confirmed
- [ ] Any media attachment verified
- [ ] Account/workspace assumptions documented
