---
title: Getting Started
type: docs
weight: 2
---

## Initialize a project

```nushell
mkdir my-project
cd my-project
qv init --nu-version ">=0.109,<0.111" # optionally specify the version(s) of Nu this project will support
```

`qv init` creates:

- `nupackage.toml`
- `<project-dir-name>/mod.nu`
- `.nu-env/`
- `.gitignore` entry for `.nu-env/`

It will download the specified version of Nu. If you didn't specify a version of Nu, it will download the Nu binary matching the version in your PATH. Quiver does this because if it used your system installation of Nu and you upgraded that, the symlink to `.nu-env/bin/` wouldn't match the version specified in the project's `nupackage.toml`.

## Add dependencies

Add a module from a full git URL:

```nushell
qv add https://github.com/freepicheep/nu-salesforce
```

Add a module using `owner/repo` shorthand (default git provider configurable in Quiver config):

```nushell
qv add freepicheep/nu-salesforce
```

Add a plugin pinned to a tag:

```nushell
qv add-plugin fdncred/nu_plugin_file --tag v0.22.0 --bin nu_plugin_file
```

Add a Nushell core plugin by alias:

```nushell
qv add-plugin polars
```

If you do not pass `--tag`, `--branch`, or `--rev` to `qv add`, Quiver will try to detect a suitable ref automatically.

## Install the environment

```nushell
qv install
```

This resolves dependencies, installs modules into `.nu-env/modules/`, installs plugin binaries when needed, and writes `quiver.lock`.

## Use the environment

Run a one-off command:

```nushell
qv run nu script.nu
```

Or enter the environment:

```nushell
qv run nu
```

The activated `nu` uses the project config and plugin registry automatically.

## Re-resolve and inspect

```nushell
qv update
qv list
```

`qv update` ignores the existing lockfile and resolves again. `qv list` shows installed dependencies for the current project.

## Remove dependencies

You can either remove dependencies directly from the `nupackage.toml` and run `qv install`, or you can run `qv rm dependency-name` and it will remove the dependency.
