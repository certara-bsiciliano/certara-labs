# certara-labs (agents)

This folder groups **three independent git repos**. When editing a file, follow the **AGENTS.md**, **CLAUDE.md**, and **`.cursor/rules`** that belong to **the repository that contains that file**. Shared umbrella rules in [.cursor/rules/](.cursor/rules/) apply across all three when this folder is the Cursor workspace root.

## Repo map

| Path | Docs to read first |
|------|-------------------|
| [coprompter/](coprompter/) | [coprompter/CLAUDE.md](coprompter/CLAUDE.md) |
| [coauthor-wiki/](coauthor-wiki/) | [coauthor-wiki/AGENTS.md](coauthor-wiki/AGENTS.md), [coauthor-wiki/CLAUDE.md](coauthor-wiki/CLAUDE.md) |
| [coauthor-testing/](coauthor-testing/) | [coauthor-testing/README.md](coauthor-testing/README.md) |

## Where to commit (git)

Each subdirectory is its **own** git repository. Commit and push **only inside the repo whose files you changed**.

| Paths you edited | Run git in |
|------------------|------------|
| [coprompter/](coprompter/) | `coprompter/` (that repo’s remote and branches) |
| [coauthor-wiki/](coauthor-wiki/) | `coauthor-wiki/` |
| [coauthor-testing/](coauthor-testing/) | `coauthor-testing/` |
| This parent folder only ([WORKSPACE.md](WORKSPACE.md), [.cursor/](.cursor/), root [AGENTS.md](AGENTS.md), [.cursorignore](.cursorignore)) | Not part of the three repos above. Either maintain a **separate** git repo at the certara-labs parent (if you `git init` here), keep these files local-only, or copy policy into a repo your team uses for shared tooling. |

Example:

```bash
cd coprompter && git status && git commit && git push
cd ../coauthor-wiki && git status
```

## Cursor rules

- **Umbrella (this folder):** [.cursor/rules/](.cursor/rules/) for shared behavior (tone, planning, commits, prose style for markdown and Python). **Start here when lost:** [.cursor/rules/workspace-orientation.mdc](.cursor/rules/workspace-orientation.mdc) points agents at [WORKSPACE.md](WORKSPACE.md) and this file. **Pre-push cleanup and which repo to commit:** [.cursor/rules/pre-push-hygiene.mdc](.cursor/rules/pre-push-hygiene.mdc) (see [Where to commit](#where-to-commit-git) below). **Typography** (em dash and double hyphen in user-facing copy and docs): [.cursor/rules/no-em-dash.mdc](.cursor/rules/no-em-dash.mdc).
- **Coprompter-only:** [coprompter/.cursor/rules/](coprompter/.cursor/rules/) for GUI and repo-specific rules when changing files under `coprompter/` (or matching paths when the workspace root is the coprompter repo alone).

### Precedence and scope

- **Umbrella rules** ([.cursor/rules/](.cursor/rules/)): apply to the whole workspace. `alwaysApply` rules run for any task; others (e.g. [no-em-dash.mdc](.cursor/rules/no-em-dash.mdc)) apply when you edit paths matched by their globs (for example `**/*.md` and `**/*.py`).
- **Coprompter rules** ([coprompter/.cursor/rules/](coprompter/.cursor/rules/)): `alwaysApply: false` with globs so they attach when files under CoPrompter match (paths like `coprompter/...` when this folder is the root, or `src/`, `tests/`, and similar when only the coprompter repo is opened). They do not target coauthor-wiki or coauthor-testing.
- **Conflict:** the repo that **owns the file** wins for product behavior; umbrella rules are global process and typography unless a repo explicitly documents an exception.

## MCP (Model Context Protocol)

Project config for this layout: [.cursor/mcp.json](.cursor/mcp.json) (reload MCP or restart Cursor after edits).

| Server | Notes |
|--------|--------|
| **ms-learn** | Remote; no local setup. |
| **github** | Set **`GITHUB_MCP_AUTHORIZATION`** in your environment to the full `Authorization` header value Cursor should send (do not commit secrets). If unset, disable or ignore the server in Cursor settings. |
| **coauthor-wiki** | Stdio server; uses [coauthor-wiki/.venv/bin/python](coauthor-wiki/) and [coauthor-wiki/wiki-mcp/server.py](coauthor-wiki/wiki-mcp/server.py). Create the venv per [coauthor-wiki/wiki-mcp/README.md](coauthor-wiki/wiki-mcp/README.md) if missing. |

**Wiki tools and behavior:** How to use `search_wiki` / `get_article` / `list_articles`, plus release-status rules, are in [coauthor-wiki/AGENTS.md](coauthor-wiki/AGENTS.md).

**Opening only one subrepo as the workspace root:** `${workspaceFolder}` in [.cursor/mcp.json](.cursor/mcp.json) points at this umbrella folder. For a **coprompter-only** or **wiki-only** window, duplicate the entries you need into **`~/.cursor/mcp.json`** with paths adjusted, or open **`certara-labs`** as the folder.

If MCP is unavailable, fall back to each repo’s docs (for the wiki: summaries index and markdown under `coauthor-wiki/wiki/`).

## Indexing

[.cursorignore](.cursorignore) trims common build and dependency trees from Cursor indexing for this workspace.
