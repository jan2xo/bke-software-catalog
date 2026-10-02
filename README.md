# BKE Software Catalog

Canonical GitHub release warehouse for BKE Digital Solutions software binaries.

## Purpose

This repository owns release distribution artifacts only. Product source code remains in each product's canonical repository; Digital Solutions remains the update/catalog authority; GitHub Releases in this repository host downloadable installers and packages.

## Release naming

Use one release tag per product version:

- `bke-licensing-agent-v<version>`
- `bke-air-stack-v<version>`
- `bke-render-dock-v<version>`

Example:

- `bke-licensing-agent-v2.0.0`

## Asset naming

Keep platform and architecture explicit and stable.

Examples:

- `BKE-Licensing-Agent-2.0.0-Windows-x64.exe`
- `BKE-Air-Stack-1.0.0-Windows-x64.zip`
- `BKE-Render-Dock-1.0.0-Windows-x64.zip`

## Authority boundary

- **Digital Solutions** decides what version is current and which exact catalog release/artifact is authorized.
- **BKE Software Catalog** stores immutable release bytes and must not rebuild product source.
- **Licensing Agent** verifies Digital Solutions policy and the exact GitHub artifact identity before privileged update/install work.
- Product repositories remain canonical for source and build/certification provenance.

## Agent PREPRODUCTION publication

Agent publication is explicit and consumes bytes already certified by the
Licensing Agent repository. The Software Catalog independently verifies the
exact Agent source SHA, successful installer certification run, Actions artifact
ID, package manifest, installer SHA-256, and byte count before publication.

PREPRODUCTION Agent releases are prereleases, are not production-ready, must not
become the repository's latest release, and must never overwrite an existing
release or tag.

Merging publication tooling does not itself authorize or perform a release.

Do not place application source code, build logic, private signing material, or
licensing authority logic in this repository.
