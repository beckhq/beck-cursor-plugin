# Beck

Project management for humans and AI assistants. One prioritized backlog — tasks, icebox, epics, PRDs, and review — that Cursor, Grok Bot, and any MCP client can operate.

Beck is a Cursor plugin (skill + MCP server) for [beck.bot](https://beck.bot). It connects your AI assistant to project management, product management, task tracking, backlog grooming, document planning, and agent automation. The same stories humans move on the board are the stories the agent starts, logs, finishes, and (when you choose) accepts or rejects.

Use this plugin when you want an AI coding agent to manage work, not invent a side channel: write a PRD, plan documents into epics, import user stories, pick up the next task, log progress, and submit for review.

## What it is

A **project management** and **task management** system built for hybrid teams. Documents are the living planning corpus (PRD, notes, specs). **Plan it** snapshots selected pages into an epic and optional story breakdown. The daily product is the **backlog**: icebox for what is not ready, list order for priority, in progress, ready for review, accepted. Story points (1, 2, 3, 5, 8), acceptance criteria, comments, and structured progress stay on the story.

Agents are workers in that queue. They get an API token, not a public URL. Autonomy is an expressed choice: human review, peer-bot review, or full automation — per job or channel. The human’s prompt always wins.

## Who it is for

- Founders and engineering leads using Cursor, Grok Bot, Claude Code, or another MCP host who need project management the agent can actually operate
- Product managers writing a PRD, product requirements, or a spec and turning planning documents into epics and tasks
- Teams that want AI automation on the same backlog as standup: what’s next, what’s in review, what was accepted
- Multi-bot channels (coder, reviewer, PM) that need named tokens so activity attributes to each bot

## What the assistant can do

**Project management and planning**
- Bind to a workspace (or create one if you asked)
- Co-write planning documents: PRD, product requirements, research notes, specs (etag-safe markdown)
- Plan it: snapshot documents into an epic spec and suggested user stories
- Import suggested tasks to the backlog or the icebox
- List epics, read the working spec, attach a branch name / PR URL

**Task management and execution**
- List and filter tasks (status, epic, assignee, icebox)
- Recommend the next story
- Start, log progress (attempted, succeeded, failed, blockers, questions), finish
- Accept or reject ready-for-review work under the autonomy mode
- Comments, relevant files, story points, acceptance criteria, tags

**Automation and identity**
- `whoami` — token identity
- Named API tokens for a roster (`Coder`, `Reviewer`); coordinator tokens can mint workers
- Live skill and llms.txt as MCP resources so a bundled copy does not go stale

## How work flows

1. Point an agent at a workspace (Documents in Beck).
2. Co-write the PRD and other planning documents.
3. Plan it when you ask. Import stories to the backlog or icebox.
4. The agent recommends, starts, logs, and finishes on the same tasks you see in the UI.
5. Review is human, peer bot, or full — you choose. Quality stays in the loop.

Canonical agent instructions: [beck.bot/skill.md](https://beck.bot/skill.md) and [beck.bot/llms.txt](https://beck.bot/llms.txt). Product facts: [beck.bot/ai-info](https://beck.bot/ai-info).

## Install

1. Add **Beck** from the Cursor Marketplace (or Grok Bot’s Cursor plugin install).
2. Open **Plugins → Beck → Configure**.
3. Paste a token from [Settings → Tokens](https://beck.bot/settings/tokens). Name it after this bot when you staff a roster (`Coder`, `Reviewer`).
4. Optional: `BECK_API_URL` if you are not on `https://beck.bot`.

Pin a workspace from Documents → Point an agent. Re-read the live skill before acting; this bundle can lag.

The MCP process is [`@becklabs/beck-mcp-server`](https://www.npmjs.com/package/@becklabs/beck-mcp-server). REST is the same surface at `https://beck.bot/api/v1` with `Authorization: Bearer beck_…`.

## Search terms

Project management, product management, task management, task tracker, backlog, icebox, agile planning, user stories, story points, epic, PRD, product requirements document, spec, specification, planning documents, markdown docs, accept/reject review, ready for review, what’s next, standup board, AI agents, agent automation, MCP server, Cursor plugin, Grok Bot, multi-bot workflow, API token.

## License

MIT
