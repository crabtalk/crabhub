# WeChat

Command service — WeChat bot gateway for agents.

```toml
[package]
name = "wechat"
description = "WeChat bot gateway for agents"
logo = "https://crabtalk.ai/logos/wechat.png"
repository = "https://github.com/crabtalk/crabtalk"
keywords = ["wechat", "bot", "gateway", "chat"]

[commands.wechat]
description = "WeChat bot gateway for agents"
crate = "crabtalk-wechat"
```

## What's happening

- **`[package]`** — Standard metadata. The `repository` is the main crabtalk
  monorepo since the wechat binary is built from it.
- **`[commands.wechat]`** — The `crabtalk-wechat` crate is auto-installed via
  `cargo install` during `hub install`. Once installed, managed via
  `crabtalk wechat start|stop|run|logs`.
