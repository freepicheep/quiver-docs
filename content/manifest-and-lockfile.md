---
title: Manifest and Lockfile
type: docs
weight: 4
---

Quiver projects are defined by `nupackage.toml` and reproduced by `quiver.lock`.

## `nupackage.toml`

The manifest has a `[package]` section and dependency groups for modules and plugins.

```toml
[package]
name = "my-module"
version = "0.1.0"
description = "Example Quiver package"
license = "MIT"
authors = ["Your Name"]
nu-version = ">=0.109,<0.111"

[dependencies.modules]
nu-utils = { git = "https://github.com/user/nu-utils", tag = "v1.0.0" }
other-lib = { git = "https://github.com/user/other-lib", branch = "main" }
pinned = { git = "https://github.com/user/pinned", rev = "a3f9c12" }

[dependencies.plugins]
nu_plugin_inc = { git = "https://github.com/nushell/nu_plugin_inc", tag = "v0.91.0", bin = "nu_plugin_inc" }
nu_plugin_polars = { source = "nu-core", bin = "nu_plugin_polars" }
```

### Module dependencies

Each module dependency must set exactly one of:

- `tag`
- `branch`
- `rev`

Each module dependency also needs a secure `git` source URL.

### Plugin dependencies

Plugin dependencies support two source modes:

- Git-based plugins with `git` plus exactly one of `tag`, `branch`, or `rev`
- `source = "nu-core"` plugins with `bin`, and no git ref fields

The optional `bin` field is used when the binary name differs from the dependency key or repository name.

## `quiver.lock`

The lockfile pins resolved commits and installation checksums. Quiver writes it automatically after installation.

```toml
version = 1

[[package]]
name = "nu-utils"
git = "https://github.com/user/nu-utils"
tag = "v1.0.0"
rev = "d4e8f1a2b3c4d5e6f7a8b9c0d1e2f3a4b5c6d7e8"
sha256 = "..."
```

Plugin entries may also include:

- `kind = "plugin"`
- `path`
- `asset_sha256`
- `asset_url`

## Resolution behavior

- `{nushell} qv install` reuses `quiver.lock` when it is present and still matches the manifest.
- `{nushell} qv install --frozen` refuses to resolve and requires a valid lockfile.
- `{nushell} qv update` deletes the local lockfile and resolves again.

Commit `quiver.lock` to version control if you want reproducible installs across machines and CI.
