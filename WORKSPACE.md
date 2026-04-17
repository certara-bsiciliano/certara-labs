# certara-labs (umbrella folder)

This directory is a convenience layout: **three separate git repositories** side by side so one Cursor window can hold related work. It is not itself a git repo.

## Repositories

| Directory | Role |
|-----------|------|
| [coprompter](coprompter/) | Desktop GUI for editing and generating CoAuthor prompts in Word (`.docx`). |
| [coauthor-wiki](coauthor-wiki/) | Product wiki (markdown), Slack bot, and stdio MCP server for wiki search. |
| [coauthor-testing](coauthor-testing/) | Local test client for CoAuthor (e.g. table extraction against dev backends). |

## Git and branches

Run **git commands inside the repo you mean** (each subdirectory has its own `.git`). For example:

```bash
cd coprompter && git status
cd ../coauthor-wiki && git status
cd ../coauthor-testing && git status
```

A table of **which paths belong to which remote** (including files only at this parent folder) is in [AGENTS.md](AGENTS.md) under **Where to commit**.

## Overlap

**coprompter** and **coauthor-testing** both touch CoAuthor workflows (prompts, extraction, dev APIs). Product behavior and terminology often come from **coauthor-wiki**; use the wiki MCP or [coauthor-wiki/AGENTS.md](coauthor-wiki/AGENTS.md) when unsure.

## Optional: multi-root workspace

To open these three folders as explicit roots in one Cursor window, you can add a `certara-labs.code-workspace` file later (VS Code / Cursor multi-root workspaces). The parent-folder layout works without it.

## Cursor (this folder)

With **`certara-labs`** as the opened folder, shared agent rules and MCP live under [`.cursor/`](.cursor/) ([`.cursor/rules/`](.cursor/rules/), [`.cursor/mcp.json`](.cursor/mcp.json)). [.cursorignore](.cursorignore) limits what Cursor indexes (dependencies, build output, etc.).

## Agents and automation

See [AGENTS.md](AGENTS.md) for pointers to per-repo docs, Cursor rules, and MCP setup.
