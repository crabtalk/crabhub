# Gstack

Agent package with an inference-based setup prompt.

```toml
[package]
name = "gstack"
version = "0.0.1"
authors = ["garrytan <garrytan@gmail.com>"]
license = "MIT"
repository = "https://github.com/crabtalk/gstack"
branch = "crabtalk"
keywords = ["agent", "stack"]
description = "garrytan's AI engineering workflow agent powered by crabtalk"

[package.setup]
prompt = "setup.md"

[agents.garrytan]
description = "AI engineering workflow agent — suggests the right skill at the right time"
thinking = true
```

## What's happening

- **`[package]`** — Uses the optional `version`, `authors`, `license`, and
  `branch` fields. `branch = "crabtalk"` tells the installer to clone that
  specific branch instead of the repo default.
- **`[package.setup]`** — The prompt variant. `setup.md` is read from the repo
  root and sent to the daemon for inference. This is useful for interactive
  setup that requires the agent's help (e.g., configuring API keys).
- **`[agents.garrytan]`** — Declares an agent with `thinking = true` for
  reasoning mode. The prompt file is discovered by convention at
  `agents/garrytan.md` in the source repo.
