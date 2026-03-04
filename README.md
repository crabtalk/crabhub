# Walrus Hub

A community registry for AI agent resources — MCP servers, skills, agents, prompts, and tools.

Resources are indexed as `scope/config.toml` files in this repository. Anyone can add resources by opening a PR.

## Index Format

Each resource lives at `<scope>/<config>.toml`:

```
microsoft/playwright.toml
anthropic/claude.toml
my-org/my-tool.toml
```

`scope` is typically the author, organization, or tool namespace. One `.toml` file can declare multiple related resources under the same scope.

### config.toml structure

```toml
[package]
name = "playwright"

[mcp_servers.playwright]
description = "Playwright MCP server"
command = "npx"
args = ["-y", "@playwright/mcp"]
keywords = ["playwright", "mcp"]

[skills.playwright-cli]
description = "CLI for common Playwright actions. Record and generate Playwright code, inspect selectors and take screenshots."
repo = "https://github.com/microsoft/playwright-cli"
path = "skills/playwright-cli"
```

Supported sections: `mcp_servers`, `skills`, `agents`.

## Example

[microsoft/playwright.toml](microsoft/playwright.toml) — MCP server and CLI skill for browser automation with Playwright.

## Add a Resource

1. Fork this repo
2. Create `<scope>/<config>.toml` following the format above
3. Open a PR — the PR template will guide you through the checklist

## License

[MIT](LICENSE)
