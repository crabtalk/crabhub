# Writing an Agent Package

An agent package bundles a system prompt, optional skills, and configuration
into an installable unit. This is how you distribute a complete agent persona.

## Minimal manifest

```toml
[package]
name = "my-agent"
description = "What the agent does"
repository = "https://github.com/org/my-agent"
keywords = ["agent"]

[agents.my-agent]
description = "One-line agent description"
```

The `repository` field is required — the installer clones it to find the
prompt file and any bundled skills.

## Prompt discovery

Agent prompts are discovered by convention. For an agent key `my-agent`, the
installer looks for `agents/my-agent.md` in the source repository and copies
it to `~/.crabtalk/local/agents/my-agent.md`.

You can also specify the path explicitly:

```toml
[agents.my-agent]
description = "One-line agent description"
prompt = "prompts/custom-path.md"
```

## Bundling skills

If your repo includes skills under a `skills/` directory, they are
auto-discovered at runtime. You can declare which skills the agent uses:

```toml
[agents.my-agent]
description = "One-line agent description"
skills = ["code-review", "deploy"]
```

## Agent options

```toml
[agents.my-agent]
description = "One-line agent description"
thinking = true          # enable reasoning mode
model = "claude-sonnet"  # model override
mcps = ["playwright"]    # MCP servers this agent can access
```

## Cloning a specific branch

If the agent lives on a non-default branch:

```toml
[package]
name = "my-agent"
repository = "https://github.com/org/my-agent"
branch = "crabtalk"
```

## Interactive setup

For agents that need configuration (API keys, preferences), use a setup prompt
instead of a shell command. The prompt is sent to the daemon for inference:

```toml
[package.setup]
prompt = "setup.md"
```

See the [Gstack](./gstack.md) example for a complete manifest.
