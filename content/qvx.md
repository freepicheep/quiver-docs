---
title: qvx
type: docs
weight: 7
---

`qvx` runs an exported command from a remote Nu module without creating a local project first.

It is useful for one-off tasks where you want Quiver to fetch the module, create a temporary environment, and invoke the command for you.

## Run a remote command

```nushell
qvx freepicheep/nu-doc-gen generate-doc-site nu-salesforce site
```

The first argument is the module source. This can be an `owner/repo` shorthand or a full git URL. The second argument is the exported command to run. Everything after that is passed to the command as arguments.

If you do not pin a ref, `qvx` tries to use the latest detected tag. If no tags are available, it falls back to the default branch.

## Pin a specific ref

Pin a tag in the source string:

```nushell
qvx freepicheep/nu-doc-gen@v1.2.0 generate-doc-site nu-salesforce .
```

Or pin it explicitly:

```nushell
qvx --tag v1.2.0 freepicheep/nu-doc-gen generate-doc-site nu-salesforce .
qvx --branch main freepicheep/nu-doc-gen generate-doc-site nu-salesforce .
qvx --rev a3f9c12 freepicheep/nu-doc-gen generate-doc-site nu-salesforce .
```

Supported flags:

- `--tag`
- `--branch`
- `--rev`
- `--nu-version`

## Choose the Nu version

You can set the Nu version requirement for the ephemeral environment:

```nushell
qvx --nu-version ">=0.109,<0.111" freepicheep/nu-doc-gen generate-doc-site nu-salesforce .
```

If `--nu-version` is not provided and the remote module contains a `nupackage.toml` with `package.nu-version`, Quiver installs and uses that version of Nu.

## How It Works

`qvx` creates a cached ephemeral environment, installs the remote module into it, starts that environment's `nu` binary, and runs a generated wrapper equivalent to:

```nushell
use nu-doc-gen *
generate-doc-site nu-salesforce .
```
