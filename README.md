# Crabtalk Hub

A community registry for AI agent resources — MCP servers, skills, agents, and commands.

Resources are indexed as `scope/config.toml` files in this repository. Anyone can add resources by opening a PR.

## Index Format

Each resource lives at `<scope>/<config>.toml`:

```
microsoft/playwright.toml
notion/notion.toml
my-org/my-tool.toml
```

`scope` is typically the author, organization, or tool namespace. One `.toml` file can declare multiple related resources under the same scope.

### Manifest Structure

Every manifest starts with a `[package]` section, followed by one or more resource sections.

```toml
[package]
name = "my-package"
description = "Short description for hub display"
logo = "https://example.com/logo.png"
repository = "https://github.com/my-org/my-package"
keywords = ["tag1", "tag2"]
```

| Field | Required | Description |
|---|---|---|
| `name` | yes | Package name |
| `description` | no | Short description for hub display |
| `logo` | no | Logo URL for hub display |
| `repository` | no | Source repository URL (required for skills) |
| `keywords` | no | Searchable tags for hub discovery |

### Resource Sections

#### `[mcps.*]` — MCP Servers

Registers an MCP server. Merged into the user's `crab.toml` on install.

```toml
[mcps.notion]
command = "npx"
args = ["-y", "@notionhq/notion-mcp-server"]
env = { NOTION_TOKEN = "" }
```

| Field | Required | Default | Description |
|---|---|---|---|
| `command` | yes* | — | Executable to spawn (stdio transport) |
| `args` | no | `[]` | Command-line arguments |
| `env` | no | `{}` | Environment variables |
| `name` | no | map key | Display name |
| `auto_restart` | no | `true` | Auto-restart on failure |
| `url` | no | — | HTTP URL for streamable HTTP transport (replaces stdio) |

*Either `command` or `url` should be set.

#### `[skills.*]` — Skills

Downloadable skill directories, copied from `package.repository` to `~/.crabtalk/skills/<key>/` on install.

```toml
[skills.playwright-cli]
description = "CLI for common Playwright actions."
path = "skills/playwright-cli"
```

| Field | Required | Description |
|---|---|---|
| `description` | yes | Skill description |
| `path` | yes | Path within the source repo to the skill directory |
| `name` | no | Display name (defaults to map key) |

#### `[agents.*]` — Agents

System prompt bundles that can declare skill dependencies. Prompt files are copied to `~/.crabtalk/agents/<key>.md` on install.

```toml
[agents.my-agent]
description = "An agent with a bundled prompt."
prompt = "prompts/my-agent.md"
skills = ["playwright-cli"]
```

| Field | Required | Description |
|---|---|---|
| `description` | yes | Agent description |
| `prompt` | yes | Path to prompt `.md` file (relative to scope dir) |
| `skills` | no | Skill keys from the same manifest to auto-install |

#### `[commands.*]` — Commands

Rust crate commands. Auto-installed via `cargo install` during `hub install`.

```toml
[commands.search]
description = "Meta-search aggregator (DuckDuckGo, Wikipedia)"
crate = "crabtalk-search"
```

| Field | Required | Description |
|---|---|---|
| `description` | yes | Human-readable description |
| `crate` | yes | Crate name on crates.io (installed via `cargo install`) |

Installed commands are managed via `crabtalk <command> start|stop|run|logs`.

## Examples

- [microsoft/playwright.toml](microsoft/playwright.toml) — MCP server and CLI skill for browser automation.
- [notion/notion.toml](notion/notion.toml) — Notion MCP server for pages, databases, and blocks.
- [vercel/agent-browser.toml](vercel/agent-browser.toml) — Browser automation CLI for AI agents.
- [crabtalk/search.toml](crabtalk/search.toml) — Meta-search aggregator command.
- [crabtalk/telegram.toml](crabtalk/telegram.toml) — Telegram bot gateway command.
- [crabtalk/wechat.toml](crabtalk/wechat.toml) — WeChat bot gateway command.

## Add a Resource

1. Fork this repo
2. Create `<scope>/<config>.toml` following the format above
3. Open a PR — the PR template will guide you through the checklist

## License

[MIT](LICENSE)
