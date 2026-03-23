# Search

Command service — registers a locally-installed binary as a managed command.

```toml
[package]
name = "search"
description = "Meta-search aggregator (Bing, Brave, DuckDuckGo, Mojeek, Wikipedia)"
logo = "https://crabtalk.ai/logos/search.png"
repository = "https://github.com/crabtalk/crabtalk"
keywords = ["search", "web", "bing", "brave", "duckduckgo", "mojeek", "wikipedia"]

[commands.search]
description = "Meta-search aggregator (Bing, Brave, DuckDuckGo, Mojeek, Wikipedia)"
crate = "crabtalk-search"
```

## What's happening

- **`[package]`** — Standard metadata. The `repository` is the main crabtalk
  monorepo since the search binary is built from it.
- **`[commands.search]`** — The `crabtalk-search` crate is auto-installed via
  `cargo install` during `hub install`. Once installed, managed via
  `crabtalk search start|stop|run|logs`.
