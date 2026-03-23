# Publishing

How to develop and publish a package to the Crabtalk Hub.

## 1. Write a manifest

Create a `<name>.toml` file following the [manifest format](./manifest.md).
Start with the `[package]` section and add the resource sections you need.

```toml
[package]
name = "my-package"
description = "What it does"
repository = "https://github.com/org/my-package"
keywords = ["relevant", "tags"]

[mcps.my-server]
command = "npx"
args = ["-y", "@scope/my-mcp-server"]
```

## 2. Test locally

Validate your manifest before publishing:

```bash
crabtalk hub test path/to/my-package.toml
```

This parses the manifest, checks that required fields are present, and verifies
that the resources can be resolved.

## 3. Submit to the hub

1. Fork the [hub repository](https://github.com/crabtalk/hub).
2. Add your manifest at `<scope>/<name>.toml`. Use your organization name or
   username as the scope.
3. Open a pull request.

```
my-org/my-package.toml
```

## Checklist

Before submitting:

- [ ] `package.name` is set
- [ ] `package.description` is clear and concise
- [ ] `package.repository` is set (required for agents and skills)
- [ ] `package.keywords` help users find your package
- [ ] `package.setup` works on a clean machine (if present)
- [ ] MCP servers start without errors
- [ ] Agent prompts exist at the expected paths in the source repo
- [ ] `crabtalk hub test` passes
