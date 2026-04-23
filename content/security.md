---
title: Security
type: docs
weight: 8
---

Quiver includes checksum verification for downloaded release assets, especially Nushell archives and plugin binaries.

## Default behavior

The default policy is fail-closed:

- installs fail when checksum data is missing
- installs fail when checksum data cannot be parsed
- installs fail when the checksum does not match the downloaded asset

Quiver looks for checksum metadata in the same release, preferring:

- `SHA256SUMS`
- `checksums.txt`
- a sidecar `<asset>.sha256` file

## Relevant flags

```nushell
qv install --frozen
qv install --allow-unsigned
qv install --no-build-fallback
```

- `--frozen` enforces lockfile-only installs and does not allow insecure overrides
- `--allow-unsigned` disables the signed-asset requirement for that install
- `--no-build-fallback` disables local cargo builds when no usable release asset is available

## Plugin install path

For plugin dependencies, Quiver attempts installation in this order:

1. Download a matching GitHub release asset for the current platform.
2. Fall back to building from source with Cargo if allowed.

Building from source is a different trust boundary than consuming a verified release artifact. If you want the strictest CI behavior, use:

```nushell
qv install --frozen --no-build-fallback
```
