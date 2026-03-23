# Manifest

Every hub package is a single TOML file with a required `[package]` section
followed by one or more resource sections: `[mcps.*]`, `[agents.*]`, and
`[commands.*]`.

```toml
[package]
name = "my-package"
description = "Short description"
repository = "https://github.com/org/repo"

[mcps.my-server]
command = "npx"
args = ["-y", "my-mcp-server"]
```

## `[package]`

Package metadata. The only required field is `name`.

| Field | Required | Default | Description |
|---|---|---|---|
| `name` | yes | — | Package name |
| `description` | no | `""` | Short description for hub display |
| `logo` | no | `""` | Logo URL for hub display |
| `repository` | no | `""` | Source repository URL (required for skills and agents) |
| `branch` | no | repo default | Branch to clone |
| `version` | no | — | Package version |
| `authors` | no | `[]` | Package authors |
| `license` | no | — | License identifier |
| `keywords` | no | `[]` | Searchable tags for hub discovery |
| `setup` | no | — | Post-install setup (see below) |

### `[package.setup]`

Run after installation. Two variants — use one or the other, not both.

**Shell command** — runs from the cached repo directory:

```toml
[package.setup]
command = "npx playwright install chromium"
```

**Inference prompt** — sent to the daemon. If the value ends with `.md`, it is
read as a file path relative to the repo root:

```toml
[package.setup]
prompt = "setup.md"
```

## `[mcps.*]`

Registers an MCP server. The map key becomes the server identifier.

```toml
[mcps.notion]
command = "npx"
args = ["-y", "@notionhq/notion-mcp-server"]
env = { NOTION_TOKEN = "" }
```

| Field | Required | Default | Description |
|---|---|---|---|
| `command` | yes* | `""` | Executable to spawn (stdio transport) |
| `args` | no | `[]` | Command-line arguments |
| `env` | no | `{}` | Environment variables |
| `name` | no | map key | Display name |
| `auto_restart` | no | `true` | Auto-restart on failure |
| `url` | no | — | HTTP URL for streamable HTTP transport |

\* Either `command` or `url` must be set. Use `command` for stdio transport,
`url` for HTTP.

## `[agents.*]`

Agent prompt bundles. Prompt files are discovered by convention from
`agents/<key>.md` in the source repository, or specified explicitly via the
`prompt` field.

```toml
[agents.garrytan]
description = "AI engineering workflow agent"
thinking = true
skills = ["agent-browser"]
```

| Field | Required | Default | Description |
|---|---|---|---|
| `description` | yes | — | Agent description |
| `prompt` | no | `""` | Path to prompt `.md` file (relative to repo root) |
| `skills` | no | `[]` | Skill names this agent can access |
| `model` | no | — | Model override for this agent |
| `thinking` | no | `false` | Enable thinking/reasoning mode |
| `mcps` | no | `[]` | MCP server names this agent can access |

## `[commands.*]`

Rust crate commands. Auto-installed via `cargo install` during `hub install`.

```toml
[commands.search]
description = "Meta-search aggregator"
crate = "crabtalk-search"
```

| Field | Required | Description |
|---|---|---|
| `description` | yes | Human-readable description |
| `crate` | yes | Crate name on crates.io (installed via `cargo install`) |

Installed commands are managed via `crabtalk <command> start|stop|run|logs`.
