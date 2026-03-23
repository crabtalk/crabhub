# Writing a Command Package

A command package registers a Rust binary crate as a managed service. The hub
installs the crate via `cargo install` and the daemon manages its lifecycle.

## Minimal manifest

```toml
[package]
name = "my-command"
description = "What the command does"
repository = "https://github.com/org/my-command"
keywords = ["relevant", "tags"]

[commands.my-command]
description = "What the command does"
crate = "crabtalk-my-command"
```

On `crabtalk hub install`, the crate is installed from crates.io via
`cargo install crabtalk-my-command`.

## Naming convention

Command binaries follow the pattern `crabtalk-<name>`. This allows the CLI to
dispatch `crabtalk <name>` to the correct binary — the same pattern Cargo uses
for subcommands.

## Lifecycle management

Once installed, commands are managed via:

```bash
crabtalk <name> start   # start the service
crabtalk <name> stop    # stop the service
crabtalk <name> run     # run in foreground
crabtalk <name> logs    # view service logs
```

## Multiple commands

A single package can declare multiple commands if they ship from the same
repository:

```toml
[commands.search]
description = "Meta-search aggregator"
crate = "crabtalk-search"

[commands.telegram]
description = "Telegram bot gateway"
crate = "crabtalk-telegram"
```

See the [Search](./search.md) and [WeChat](./wechat.md) examples for complete
manifests.
