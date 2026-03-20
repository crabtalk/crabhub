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

### config.toml structure

```toml
[package]
name = "my-package"
repository = "https://github.com/my-org/my-package"

[mcps.my-mcp]
command = "npx"
args = ["-y", "@my-org/mcp"]

[skills.my-skill]
description = "A downloadable skill."
path = "skills/my-skill"

[agents.my-agent]
description = "An agent with a bundled prompt."
prompt = "prompts/my-agent.md"
skills = ["my-skill"]

[commands.my-command]
description = "A locally-installed command service."
binary = "my-binary"
subcommand = "serve"
```

Supported sections: `mcps`, `skills`, `agents`, `commands`.

## Examples

- [microsoft/playwright.toml](microsoft/playwright.toml) — MCP server and CLI skill for browser automation with Playwright.
- [notion/notion.toml](notion/notion.toml) — Notion MCP server for pages, databases, and blocks.
- [vercel/agent-browser.toml](vercel/agent-browser.toml) — Browser automation CLI for AI agents.
- [crabtalk/search.toml](crabtalk/search.toml) — Meta-search aggregator command.
- [crabtalk/telegram.toml](crabtalk/telegram.toml) — Telegram bot gateway command.

## Add a Resource

1. Fork this repo
2. Create `<scope>/<config>.toml` following the format above
3. Open a PR — the PR template will guide you through the checklist

## License

[MIT](LICENSE)
