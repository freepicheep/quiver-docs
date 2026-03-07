---
title: Introduction
type: docs
toc: true
weight: 1
---

Quiver is a Rust CLI for managing Nushell modules and plugins distributed as git repositories. It handles dependency resolution, fetching, lockfiles, and project-local environment setup for Nushell projects.

{{< cards cols="2" >}}
  {{< card link="getting-started" title="Getting Started" icon="academic-cap" >}}
  {{< card link="installation" title="Installation" icon="download" >}}
  {{< card link="commands" title="Commands" icon="terminal" >}}
  {{< card link="manifest-and-lockfile" title="Manifest and Lockfile" icon="document-text" >}}
  {{< card link="environment-and-activation" title="Environment and Activation" icon="sparkles" >}}
  {{< card link="global-config" title="Global Config" icon="cog" >}}
  {{< card link="security" title="Security" icon="shield-check" >}}
  {{< card link="architecture" title="Architecture" icon="cube" >}}
{{< /cards >}}

## What Quiver Does

- Resolves module and plugin dependencies from git repositories
- Installs dependencies into a project-local `.nu-env/` environment
- Writes `quiver.lock` with pinned revisions and checksums
- Reuses shared caches so repeated installs are fast
- Generates shell and editor integration for Nushell workflows

## Install

Install a released build with one of these options:

```nushell
brew install freepicheep/tap/quiver
```

```nushell
mise use -g github:freepicheep/quiver
```

```nushell
curl --proto '=https' --tlsv1.2 -LsSf https://github.com/freepicheep/quiver/releases/latest/download/quiver-installer.sh | sh
```

Or build from source:

```nushell
cargo install --git https://github.com/freepicheep/quiver
```

## Quick Start

```nushell
qv init --nu-version ">=0.109,<0.111"
qv add freepicheep/nu-salesforce
qv add-plugin polars
qv install
qv run nu
```

## How It Works

A Quiver project centers around these files:

- `nupackage.toml` declares package metadata and dependencies
- `<project-dir-name>/mod.nu` is the Nushell module entry point
- `quiver.lock` pins exact commits and checksums
- `.nu-env/` contains the generated local environment

Running `qv init` or `qv install` prepares a local environment that looks like this:

```text
.nu-env/
├── activate.nu
├── config.nu
├── plugins.msgpackz
├── bin/
│   └── nu
└── modules/
```

Quiver also keeps shared installs outside the project so multiple repos can reuse the same git cache, plugin binaries, and Nushell versions.

## Common Commands

```nushell
qv init
qv add owner/repo
qv add-plugin nushell/nu_plugin_inc --tag v0.91.0 --bin nu_plugin_inc
qv install
qv install --frozen
qv update
qv list
qv hook
qv lsp
```

## Next Pages

If you are new to the tool, continue with [Getting Started](getting-started). If you need the file formats, go to [Manifest and Lockfile](manifest-and-lockfile). If you want implementation details, go to [Architecture](architecture).
