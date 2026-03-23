# Overview

The Crabtalk Hub is a community registry for AI agent resources — MCP servers,
skills, agents, and commands. Resources are indexed as TOML manifests in the
[hub repository](https://github.com/crabtalk/hub) and installed via the
`crabtalk` CLI.

## Index Layout

Each manifest lives at `<scope>/<name>.toml`:

```
microsoft/playwright.toml
notion/notion.toml
crabtalk/search.toml
```

`scope` is typically the author, organization, or tool namespace. A single
`.toml` file can declare multiple related resources under the same package.

## Installation

```bash
crabtalk hub install scope/name
```

This:

1. Fetches the manifest from the hub index.
2. Clones the source repository (if `package.repository` is set) to
   `~/.crabtalk/.cache/repos/<slug>/`.
3. Copies the manifest to `~/.crabtalk/packages/<scope>/<name>.toml`.
4. Merges resource definitions (MCP servers, agents, commands) into the user's
   `crab.toml`.
5. Runs `[package.setup]` if present.

## Directory Conventions

| Path                        | Purpose                                               |
| --------------------------- | ----------------------------------------------------- |
| `~/.crabtalk/packages/`     | Installed package manifests                           |
| `~/.crabtalk/config/`       | Service configuration files (`.toml`)                 |
| `~/.crabtalk/.cache/repos/` | Cached source repository clones                       |
| `~/.crabtalk/local/agents/` | Agent prompt files (`.md`)                            |
| `~/.crabtalk/local/skills/` | Installed skill directories (auto-loaded)             |
| `~/.crabtalk/config.toml`   | Runtime configuration (MCP servers, agents, commands) |

## Skill Discovery

Skills are auto-loaded — no manifest registration required. Crabtalk scans two
locations for skill directories:

1. **Local skills** — `~/.crabtalk/local/skills/<name>/`
2. **Package skills** — `~/.crabtalk/.cache/repos/<slug>/skills/<name>/`

Any directory containing a `SKILL.md` file is picked up automatically. Skills
follow the [agentskills](https://agentskills.dev) standard and are invoked via
`/skill-name` in the REPL.
