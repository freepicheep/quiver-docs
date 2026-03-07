---
title: Environment and Activation
type: docs
weight: 5
---

Upon project initialization or installation, Quiver creates a project-local environment in `.nu-env/`.

## Directory layout

```text
.nu-env/
├── activate.nu
├── config.nu
├── plugins.msgpackz
├── bin/
│   └── nu
└── modules/
```

Key pieces:

- `activate.nu` loads the environment as an overlay and provides `deactivate`
- `config.nu` sets Nushell library and plugin directories
- `plugins.msgpackz` is the plugin registry/config used by Nushell
- `bin/nu` points to the Nushell version selected for the project
- `modules/` contains installed module dependencies

## Running Scripts or Entering the Nu REPL for The Environment

For most automation and scripting, `qv run` is the simplest entrypoint.

```nushell
# run a specific script with all the dependencies loaded (including plugins)
qv run nu script.nu
```

```nushell
# run the nu version in .nu-env/bin/ with the package environment
qv run nu
```

### Overlay activation

You can also use the overlay:

```nushell
overlay use .nu-env/activate.nu
# and run nu with the alias supplied by `activate.nu`
nu
```

Leave the shell with `exit`, then unload the overlay with `deactivate`.

## LSP configuration

Quiver can also generate editor-specific Nushell LSP settings:

```nushell
qv lsp
qv lsp --editor helix --editor zed
```

There are currently only presets for Helix and Zed.

## Auto-activation hook

Quiver can print a Nushell hook that updates environment state when you `cd` into or out of a project.

```nushell
mkdir ($nu.default-config-dir | path join "vendor" "autoload")
qv hook | save -f ($nu.default-config-dir | path join "vendor" "autoload" "quiver_hook.nu")
```

This hook is useful for keeping `$env.NU_LIB_DIRS` in sync with the current project. For the full overlay behavior, use `overlay use .nu-env/activate.nu`.
