---
title: Installation
type: docs
weight: 1
---

Quiver ships as a standalone CLI. The binary name shown in the codebase is `qv`.

## Install a released build

```nushell
brew install freepicheep/tap/quiver
```

```nushell
mise use -g github:freepicheep/quiver
```

```nushell
curl --proto '=https' --tlsv1.2 -LsSf https://github.com/freepicheep/quiver/releases/latest/download/quiver-installer.sh | sh
```

## Build from source

```nushell
cargo install --git https://github.com/freepicheep/quiver
```

## Verify the install

```nushell
qv --version
```

After Quiver is installed, continue with [Getting Started](getting-started).
