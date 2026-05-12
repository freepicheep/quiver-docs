---
title: Global Config
type: docs
weight: 6
---

Global configuration lives at `~/.config/quiver/config.nuon`.

Use it for:

- global module installs
- global plugin installs
- default git provider selection for `owner/repo` shorthand
- install mode defaults
- security defaults

## Example

```nu
{
  default_git_provider: github,
  install_mode: clone,
  security: {
    require_signed_assets: true
  },
  modules: {
    nu-repl-command-info: {
      git: "https://github.com/Bahex/nu-repl-command-info.git",
      branch: main
    },
    nu-salesforce: {
      git: "https://github.com/freepicheep/nu-salesforce",
      tag: "v0.3.2"
    }
  }
}
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
