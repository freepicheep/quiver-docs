---
title: Architecture
type: docs
weight: 8
---

Quiver is a single-crate Rust CLI. The codebase is intentionally split into focused modules under `src/`.

## High-level flow

```text
nupackage.toml
  -> resolver
  -> installer
  -> .nu-env/modules
  -> quiver.lock
```

At install time, the flow is:

1. Parse `nupackage.toml`.
2. Resolve module and plugin dependencies to exact commits.
3. Fetch repository data and release assets as needed.
4. Materialize modules into `.nu-env/modules/` or the global modules directory.
5. Compute deterministic SHA-256 checksums.
6. Write `quiver.lock` or `config.lock`.

## Source modules

- `main.rs`: dispatches CLI subcommands
- `cli.rs`: clap-based command definitions
- `manifest.rs`: manifest parsing and validation
- `lockfile.rs`: lockfile parsing and serialization
- `resolver.rs`: dependency resolution and conflict detection
- `installer.rs`: install/update orchestration, plugin fetch/build flow, `.nu-env` generation
- `git.rs`: git fetch, clone, ref, and export behavior
- `checksum.rs`: directory hashing
- `config.rs`: global configuration and install path helpers
- `nu.rs`: Nushell version requirement parsing
- `error.rs`: shared error types

## Runtime paths

- Git cache: `~/.local/share/quiver/installs/git/`
- Shared plugins: `~/.local/share/quiver/installs/plugins/`
- Shared Nushell versions: `~/.local/share/quiver/installs/nu_versions/`
- Project modules: `.nu-env/modules/`
- Global modules: platform config dir under `nushell/vendor/quiver/modules/`

## Design constraints

- Dependencies are git-based rather than registry-based.
- Conflicting dependency resolutions are treated as errors.
- Lockfiles pin commits and checksums for reproducibility.
- Standard user-facing output goes to stderr, leaving stdout available for structured output and generated hooks.
