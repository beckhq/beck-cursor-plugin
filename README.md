# Beck Cursor plugin

Skill + MCP for [Beck](https://beck.bot): documents, Plan it, a shared backlog, and named bot tokens. Works in Cursor and in Grok Bot installs that use the Cursor Marketplace.

The MCP process is [`@becklabs/beck-mcp-server`](https://www.npmjs.com/package/@becklabs/beck-mcp-server). Auth is a bearer token. Hosted MCP + OAuth is the next slice.

## Two folders, same files

Edit **here** in the Beck app repo (`plugins/beck`). The public Marketplace repo is a **sibling checkout**, not a git repo nested inside this one.

| Where | Path | Git remote |
|---|---|---|
| You edit | `~/workspace/beck/plugins/beck` | `unsugarcoat/beck` |
| You publish | `~/workspace/beck-cursor-plugin` (repo **root**) | `beckhq/beck-cursor-plugin` |

After you change files in `plugins/beck`, copy them over and commit in the sibling:

```bash
# from ~/workspace/beck
./scripts/sync-cursor-plugin.sh
cd ~/workspace/beck-cursor-plugin
git add . && git status
git commit -m "Sync plugin from unsugarcoat/beck"
git push
```

Do not run `git init` inside `plugins/beck`. That nests a second `.git` in the app repo.

### One-time: create the public repo

```bash
gh repo create beckhq/beck-cursor-plugin --public \
  --description "Beck Cursor plugin — skill + MCP for documents, Plan it, and the backlog"
gh repo clone beckhq/beck-cursor-plugin ~/workspace/beck-cursor-plugin
cd ~/workspace/beck
./scripts/sync-cursor-plugin.sh
cd ~/workspace/beck-cursor-plugin
git add . && git commit -m "Beck Cursor plugin 1.1.0" && git push -u origin main
```

Then submit `https://github.com/beckhq/beck-cursor-plugin` at [cursor.com/marketplace/publish](https://cursor.com/marketplace/publish).

When the bundle changes, bump `version` in `.cursor-plugin/plugin.json` before syncing. Keep `skills/beck/SKILL.md` identical to the hosted skill (`/skill.md`); the app repo tests that.

## Install

### Local (now)

From this folder (or a clone of the public plugin repo):

```bash
mkdir -p ~/.cursor/plugins/local
ln -sfn "$(pwd)" ~/.cursor/plugins/local/beck
```

Reload Cursor (`Developer: Reload Window`). Open **Customize** and confirm the Beck skill and MCP server.

Then **Plugins → Beck → Configure**:

| Variable | Required | What to paste |
|---|---|---|
| `BECK_API_TOKEN` | Yes | Token from [Settings → Tokens](https://beck.bot/settings/tokens). Name it after this bot when staffing a roster. |
| `BECK_API_URL` | No | Defaults to `https://beck.bot` |

Pin a workspace from Documents → Point an agent. Agents should re-read [https://beck.bot/skill.md](https://beck.bot/skill.md); the bundled skill goes stale.

On Teams/Enterprise, local imports may be off under Dashboard → Settings → Security → Marketplace and Plugins.

### Marketplace (after listing)

Customize → search **Beck** → Install → Configure the token as above.

Until then, submit the public repo at [cursor.com/marketplace/publish](https://cursor.com/marketplace/publish).

## What ships

| Path | Role |
|---|---|
| `.cursor-plugin/plugin.json` | Manifest, logo, token variables |
| `mcp.json` | `npx -y @becklabs/beck-mcp-server` |
| `skills/beck/SKILL.md` | Workflows (bind, autonomy, bot tokens, Plan it, execute) |
| `assets/logo.svg` | Marketplace logo |

## License

MIT
