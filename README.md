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

- `bke-licensing-agent-v1.0.0`

## Asset naming

Keep platform and architecture explicit and stable.

Examples:

- `BKE-Licensing-Agent-1.0.0-Windows-x64.exe`
- `BKE-Air-Stack-1.0.0-Windows-x64.zip`
- `BKE-Render-Dock-1.0.0-Windows-x64.zip`

## Authority boundary

- **Digital Solutions** decides what version is current and which catalog asset URL is offered.
- **BKE Software Catalog** stores release assets.
- **Licensing Agent** checks Digital Solutions, not GitHub HTML, then downloads the exact catalog URL returned by the API.
- Product repositories remain canonical for source code.

Do not place application source code or licensing authority logic in this repository.
