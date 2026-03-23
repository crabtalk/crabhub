# Playwright

MCP server with a post-install setup command.

```toml
[package]
name = "playwright"
description = "Browser automation with Playwright MCP server and CLI tools"
logo = "https://crabtalk.ai/logos/playwright.png"
repository = "https://github.com/microsoft/playwright-cli"
keywords = ["playwright", "browser", "automation", "mcp"]

[package.setup]
command = "npx playwright install chromium"

[mcps.playwright]
command = "npx"
args = ["-y", "@playwright/mcp"]
```

## What's happening

- **`[package]`** — Standard metadata. `repository` points to the source repo
  (used if the package also declares skills).
- **`[package.setup]`** — After install, runs `npx playwright install chromium`
  to download the browser binary. This is the shell command variant of setup.
- **`[mcps.playwright]`** — Registers an MCP server using stdio transport. On
  install, this config is merged into the user's `crab.toml`. The server spawns
  via `npx -y @playwright/mcp`.
