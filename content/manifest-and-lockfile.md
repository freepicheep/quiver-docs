---
title: Manifest and Lockfile
type: docs
weight: 4
---

Quiver projects are defined by `nupackage.nuon` and reproduced by `quiver.lock`.

## `nupackage.nuon`

The manifest has a `[package]` section and dependency groups for modules and plugins.

```nu
{
  package: {
    name: "rate-change-work",
    version: "0.2.4",
    description: "An example project",
    authors: ["Me"],
    nu-version: ">=0.112.2",
  },
  dependencies: {
    modules: {
      nu-salesforce: { git: "https://github.com/freepicheep/nu-salesforce", tag: "v0.3.2" },
    },
    plugins: {
      nu_plugin_polars: { source: "nu-core", bin: "nu_plugin_polars" },
    },
  },
}
```

### Module dependencies

Each module dependency must set exactly one of:

- `tag`
- `branch`
- `rev`

Each module dependency also needs a secure `git` source URL.

### Plugin dependencies

Plugin dependencies support two source modes:

- Git-based plugins with `git` plus exactly one of `tag`, `branch`, or `rev`
- `source = "nu-core"` plugins with `bin`, and no git ref fields

The optional `bin` field is used when the binary name differs from the dependency key or repository name.

## `quiver.lock`

The lockfile pins resolved commits and installation checksums. Quiver writes it automatically after installation.

```nu
# This file is generated automatically. Do not edit.
{
  version: 1,
  packages: [
    {
      name: "nu-salesforce",
      git: "https://github.com/freepicheep/nu-salesforce",
      tag: "v0.3.2",
      rev: "68ade5f59f20645b3ddc959ce4a497dab39dc68b",
      sha256: "cbcd3656edd39927af8cd5fa8faea0e9f8878814f604a862816835100fc6342e",
    },
    {
      name: "nu_plugin_polars",
      kind: "plugin",
      git: "nu-core",
      rev: "nu-0.112.2",
      path: "nu_plugin_polars",
      sha256: "91758d8a9160ab7eb1e5af5a26f3990a2bb9e157bbb1c0edecaabd32ce8803e7",
    },
  ],
}
```

Plugin entries may also include:

- `kind = "plugin"`
- `path`
- `asset_sha256`
- `asset_url`

## Resolution behavior

- `{nushell} qv install` reuses `quiver.lock` when it is present and still matches the manifest.
- `{nushell} qv install --frozen` refuses to resolve and requires a valid lockfile.
- `{nushell} qv update` deletes the local lockfile and resolves again.

Commit `quiver.lock` to version control if you want reproducible installs across machines and CI.
