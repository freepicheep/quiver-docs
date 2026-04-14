---
title: Commands
type: docs
weight: 3
---

## Project setup

### `qv init`

Create a new `nupackage.toml` in the current directory and scaffold the initial module and environment files.

```nushell
qv init --name my-module --version 0.1.0 --nu-version 0.110.0
```

Supported flags:

- `--name`
- `--version`
- `--nu-version`
- `--description`

### `qv add`

Add a module dependency from a git URL or shorthand.

```nushell
qv add owner/repo --tag v1.2.3
qv add https://git.example.com/team/mod --branch main
```

Supported flags:

- `-g`, `--global`
- `--tag`
- `--rev`
- `--branch`

### `qv add-plugin`

Add a plugin dependency from git or a supported Nushell core plugin alias.

```nushell
qv add-plugin nushell/nu_plugin_inc --tag v0.91.0 --bin nu_plugin_inc
qv add-plugin polars
```

Supported flags:

- `-g`, `--global`
- `--tag`
- `--rev`
- `--branch`
- `--bin`

### `qv remove`

Remove a dependency from the project manifest or the global config.

```nushell
qv remove nu-salesforce
qv rm nu-salesforce
qv remove -g nu-utils
```

## Install and update

### `qv install`

Install project dependencies from `nupackage.toml`.

```nushell
qv install
qv install --frozen
qv install --allow-unsigned
qv install --no-build-fallback
```

Supported flags:

- `-g`, `--global`
- `--frozen`
- `--allow-unsigned`
- `--no-build-fallback`

`--frozen` uses the lockfile only and fails if it is missing or stale.

### `qv update`

Discard the current local lockfile and resolve again.

```nushell
qv update
```

## Working in the environment

### `qv run`

Run a command inside the current project environment.

```nushell
qv run nu
qv run nu script.nu --flag
```

### `qv hook`

Print the Nushell hook used for directory-based auto-activation.

```nushell
qv hook
```

### `qv lsp`

Generate editor configuration for Nushell language server support.

```nushell
qv lsp
qv lsp --editor helix --editor zed
```

## Informational commands

### `qv list`

List installed dependencies. In a project directory it shows project-local dependencies. Without a local manifest, it falls back to global modules.

```nushell
qv list
qv ls
```

### `qv version`

Print the Quiver version.

```nushell
qv version
qv --version
qv -v
```
