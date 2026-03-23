# Writing an MCP Server Package

An MCP server package registers an external tool server that the daemon
connects to at runtime. This is the most common package type — wrapping an
existing MCP server for one-command installation.

## Minimal manifest

```toml
[package]
name = "my-server"
description = "What the server does"
keywords = ["relevant", "tags"]

[mcps.my-server]
command = "npx"
args = ["-y", "@scope/my-mcp-server"]
```

That's it. On `crabtalk hub install`, this config is merged into the user's
`config.toml` and the server starts automatically.

## Choosing a transport

MCP servers connect via **stdio** or **HTTP**. Use one or the other.

**Stdio** (most common) — the daemon spawns the process directly:

```toml
[mcps.my-server]
command = "npx"
args = ["-y", "@scope/my-mcp-server"]
```

**HTTP** — the server runs independently and the daemon connects to it:

```toml
[mcps.my-server]
url = "http://localhost:3000/mcp"
```

## Environment variables

If the server needs API keys or configuration, declare them with empty defaults.
The user fills them in after install:

```toml
[mcps.notion]
command = "npx"
args = ["-y", "@notionhq/notion-mcp-server"]
env = { NOTION_TOKEN = "" }
```

## Post-install setup

If the server needs a setup step (e.g., downloading browser binaries), add
`[package.setup]`:

```toml
[package.setup]
command = "npx playwright install chromium"
```

See the [Playwright](./playwright.md) example for a complete manifest.
