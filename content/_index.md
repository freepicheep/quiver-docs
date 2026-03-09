---
title: Introduction
type: docs
toc: true
weight: 1
description: "Quiver is a fast Nu package and project manager, written in Rust."
---

Quiver is an extremely fast Nu project and package manager. It installs Nu modules and plugins distributed as git repositories. It handles dependency resolution, fetching, lockfiles, and project-local environment setup for Nushell projects.

{{< cards cols="2" >}}
  {{< card link="getting-started" title="Getting Started" icon="academic-cap" >}}
  {{< card link="installation" title="Installation" icon="download" >}}
  {{< card link="commands" title="Commands" icon="terminal" >}}
  {{< card link="manifest-and-lockfile" title="Manifest and Lockfile" icon="document-text" >}}
  {{< card link="environment-and-activation" title="Environment and Activation" icon="cube" >}}
  {{< card link="global-config" title="Global Config" icon="cog" >}}
  {{< card link="security" title="Security" icon="shield-check" >}}
  {{< card link="architecture" title="Architecture" icon="square-3-stack-3d" >}}
{{< /cards >}}

## What Quiver Does

Quiver takes inspiration from tools like [uv](https://docs.astral.sh/uv/) for Python and creates a similar experience for managing Nu projects and modules. 
- Supports specifying a specific version of Nu for a project, managing both the installation and loading the environment with that version of Nu
- Resolves module and plugin dependencies from git repositories
- Installs dependencies into a project-local `.nu-env/` environment
- Writes `quiver.lock` with pinned revisions and checksums for reproducible environments
- Reuses shared caches so repeated installs are fast
- Simply `qv run` on a script in your package to run it with the full environment or enter the environment shell with `qv run nu` with plugins and modules ready to use
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
mkdir my-project
cd my-project

# initialize the project, optionally specifying the version of Nu
qv init --nu-version ">=0.111.0"

# add modules from GitHub repos (or full url for any git provider)
qv add freepicheep/nu-salesforce

# add plugins, including core plugins
qv add-plugin polars

# install everything and enter the shell with everything ready to use
qv install

# run a specific script in your project
qv run my-project/reformat_accounts.nu

# or enter the Nu REPL with your project's dependencies ready to use
qv run nu
```

## How It Works

A Quiver project centers around these files:

- `nupackage.toml` declares package metadata and dependencies
- `.nu-env/` contains the generated local environment
- `quiver.lock` pins exact commits and checksums

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

Quiver also keeps shared installs outside the project in the quiver store so multiple repos can reuse the same git cache, plugin binaries, and Nushell versions.

## Next Pages

If you are new to Quiver, continue with [Getting Started](getting-started). If you need help with the file formats, go to [Manifest and Lockfile](manifest-and-lockfile). If you want implementation details, go to [Architecture](architecture).
