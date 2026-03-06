---
title: Global Config
type: docs
weight: 6
---

Global configuration lives at `~/.config/quiver/config.toml`.

Use it for:

- global module dependencies
- default git provider selection for `owner/repo` shorthand
- install mode defaults
- security defaults

## Example

```toml
default_git_provider = "github"
install_mode = "clone"

[dependencies]
nu-utils = { git = "https://github.com/user/nu-utils", tag = "v1.0.0" }

[security]
require_signed_assets = true
```

## Keys

### `default_git_provider`

Supported aliases:

- `github`
- `gitlab`
- `codeberg`
- `bitbucket`

You can also use a custom host such as `git.example.com` or a full base URL such as `https://git.example.com`.

### `install_mode`

Supported values:

- `clone`
- `hardlink`
- `copy`

On Windows the default is `hardlink`. On macOS and Linux the default is `clone`.

### `modules_dir`

Optional override for the directory where global modules are installed. If omitted, Quiver uses the platform Nushell config area under `vendor/quiver/modules/`.

### `security.require_signed_assets`

Controls whether Quiver requires checksum metadata for downloaded release assets by default.

## Global installs

Install from the global config with:

```nushell
qv install -g
```

The global lockfile is written to `~/.config/quiver/config.lock`.
