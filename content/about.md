---
title: About
toc: false
---

Quiver is a module and plugin manager for [Nushell](https://www.nushell.sh/), written in Rust. It is built around a small set of project files:

- `nupackage.nuon` declares package metadata and dependencies.
- `quiver.lock` records the exact commits and checksums that were installed.
- `.nu-env/` contains the generated project environment, including module paths, plugin config, and a project-specific `nu` entrypoint.

The project is intentionally narrow in scope. Quiver does not host packages or define a centralized registry. Dependencies are fetched from git repositories, resolved to exact commits, and installed into a Nushell-friendly layout. Hopefully we can add a registry in the future.

If you are new to the tool, start with [Getting Started](getting-started). If you want the implementation model, go to [Architecture](architecture).
