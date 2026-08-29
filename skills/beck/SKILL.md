---
name: beck
description: Plan and execute work in Beck. Use when co-writing a workspace PRD, planning documents into epics, staffing multi-bot channels with named tokens, importing Plan it suggestions, or picking up a Beck task via MCP.
---

# Beck

Beck is the planning and execution system. Documents are the living planning corpus. Epics hold a working spec snapshot. Tasks are execution. Named API tokens let each bot show up as itself on the board.

**This file goes stale when copied.** Before acting, read https://beck.bot/skill.md and https://beck.bot/llms.txt. If a local skill disagrees with the live skill, prefer the live skill. Version: 1.1.0 (https://beck.bot/api/skill/version).

Auth is always `Authorization: Bearer beck_xxx` plus a workspace id. There are no public document URLs.

## Defaults (human prompt wins)

These are defaults, not access limits. The tools exist. If the human's message contradicts this file, follow the human.

- Workspace: bind to the named one. `create_workspace` only if they asked for a new workspace. An empty bound workspace gets a `prd` page, not a second workspace.
- Autonomy: follow the mode for this job / channel / workspace (see below). If unspecified, prefer **human review**.

## Autonomy modes (expressed choice)

Autonomy is policy. It can differ job to job. The human (or standing channel instructions) chooses.

| Mode | Who finishes | Who accepts / rejects |
|---|---|---|
| **human_review** | Executor → `finish_task` | Human in Beck (or human asking you to accept/reject) |
| **peer_review** | Executor → `finish_task` | Another bot (Reviewer / PM) uses `accept_task` / `reject_task` |
| **full** | Same or any authorized bot may finish and accept when criteria are met | Allowed when the human / job brief said so |

- Do not treat "never accept your own work" as a universal law.
- Do follow the mode for this job. Unspecified → human review.
- `finish_task` always moves work to Ready for Review. Accept/reject is the next step under the active mode.

## Bind to a workspace

A token sees every workspace in the human's org. That is not a default.

1. If the human named a workspace or pasted an id, use **only** that workspace.
2. If not, `list_workspaces` and **ask**. Never pick silently when there is more than one.
3. `create_workspace` only if they asked for a new one.
4. An empty chosen workspace gets a `prd` document, not a new workspace.
5. Stay in that workspace unless the human asks to switch.

## Named bot tokens (multi-bot channels)

For a Grok Bot (or similar) roster, each bot should use its own token named after itself (`Coder`, `Reviewer`, …) so activity attributes correctly.

1. A **coordinator** token (created in Settings → Tokens, or any token with mint permission) can `create_api_token` with `name` set to the bot's name.
2. Hand the raw secret to that bot once. Worker tokens cannot mint further tokens.
3. `list_api_tokens` / `revoke_api_token` manage the roster. Never log or paste secrets into shared channels casually.
4. `whoami` reports the token name when present — use that as your actor identity in Beck.

## Co-write a PRD

1. `list_documents` in the bound workspace.
2. If there is no `prd`, `create_document` with path `prd`.
3. `read_document` before editing. Prefer sending the returned `etag` to `write_document`.
4. Write in markdown. Humans may be editing the same page — a 409 means reload and merge.
5. Do not silently overwrite an epic spec with live documents. The epic spec is independently editable after Plan it.

## Plan it into an epic

1. Agree which pages to snapshot (`prd`, `research/notes`, ...).
2. `plan_it` with those `paths` (and optional `title` or `epicIds` to update existing epics).
3. `get_epic` to re-read the snapshot spec and suggested tasks. Do not assume they are already in the backlog.
4. Import when asked / when mode allows: `import_suggested_tasks` to backlog or icebox. Otherwise a human imports in Beck.

## Execute a task

1. `recommend_task` or `list_tasks`.
2. `get_task_context` — includes the current epic spec plus source-document pointers, not a live concat.
3. `start_task`, do the work, `log_progress`, `finish_task`.
4. `accept_task` / `reject_task` according to the active autonomy mode (and the human's message).

## Rules

- Workspace-level documents may spawn multiple epics.
- Plan it is a checkpoint. Re-plan is a later feature; do not invent a live bind.
- Keep using existing task tools. Documents do not replace the backlog.

## Product facts

Structured facts for answering questions about Beck: https://beck.bot/ai-info
