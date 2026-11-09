> **Updated release path (2026-11-09):** This document preserves the original macOS-only pilot proof. The current catalog publisher also requires and distributes the exact Windows x64 artifact from the same CI run. See [dual-platform artifact and parity checkpoint](media-organizer-dual-platform-beta.md) for the updated contract. Do not dispatch with only the macOS artifact inputs.

# BKE Media Organizer — PREPRODUCTION prerelease pilot

## Intent and authority

GitHub [BKE Software Catalog](https://github.com/jan2xo/bke-software-catalog) distributes immutable product bytes only; [BKE Metadata Manager](https://github.com/jan2xo/bke-metadata-manager) owns app builds, source and test certification. This path is an explicitly dispatched **PREPRODUCTION** macOS ARM64 beta distribution path. It **never** signs with an Apple Developer ID, notarizes, rebuilds product code, changes Digital Solutions catalog policy, or claims a trusted commercial release.

The existing macOS application is **ad-hoc signed** by `scripts/package-macos.sh` in the source repository, not Apple Developer ID signed. Gatekeeper may require first-launch approval. Distribution is for beta testing and machine-specific UX acceptance; it is not a substitute for signing/notarization.

## Exact pilot fixture (verified GitHub state on 2026-11-09)

- Source SHA: `363db36a56fe0a19b942eb783124f3b8ed314419`
- Product PR: [#2](https://github.com/jan2xo/bke-metadata-manager/pull/2), draft, unmerged; hardware QA still outstanding.
- CI run: [42181080912](https://github.com/jan2xo/bke-metadata-manager/actions/runs/42181080912), attempt `1`, five successful jobs (macOS, Windows, Linux test/build; macOS ARM64, Windows x64 publishing).
- macOS artifact ID: `13485089192`, name `BKE-Media-Organizer-macOS-ARM64`
- GitHub Actions archive SHA-256: `56740d23f2d79e3f3394dcb5e038d1d0b65a2e9ac4ad4d1f3a0f969bddba60f5`.
- Expected contents: `BKE-Media-Organizer-macOS-ARM64.dmg`, `BKE-Media-Organizer-macOS-ARM64.zip`.

The archive SHA-256 is NOT either inner distributable's SHA-256; compute and verify the individual final file digests during publication.

## Owner-controlled prerequisites

1. Configure **only** the Software Catalog repository secret `MEDIA_ORGANIZER_ARTIFACT_READ_TOKEN`: a short-lived, fine-grained owner token with only `Actions: read` on `jan2xo/bke-metadata-manager`. Never put it in source, PR comments, workflow inputs, or release notes. The catalog's built-in `GITHUB_TOKEN` writes only the catalog release.
2. Validate the exact source/run/artifact identifiers against the active candidate. Do not use a moving branch or rebuild the app inside the catalog.
3. The publisher must **explicitly** dispatch `Publish Media Organizer PREPRODUCTION release` on the **catalog main** branch using `PUBLISH_MEDIA_ORGANIZER_PREPRODUCTION`. Mere PR/branch push must not publish. A dispatch is separate from workflow implementation/merge approval.
4. No existing release/tag can be overwritten. New tag example: `bke-media-organizer-v1.0.0-beta.1`, prerelease only, never latest.
5. CI cannot prove native compositor blur, responsive sizing, Finder drag/drop, file collision safety with real camera footage or same-/cross-volume behavior. Record actual Mac acceptance before declaring production readiness.

## Security and publication invariant

Exact run SHA + attempt + five required successful jobs + exact artifact name/ID + GitHub-reported immutable archive digest must match; downloaded bytes must match the expected digest. Only the two expected top-level macOS files may pass intake. The source archive is never executed. Each final file digest/size is recorded in a JSON provenance manifest. Publication uploads the original exact DMG and ZIP unchanged, then re-downloads them to verify hashes/size. Release metadata must say `PREPRODUCTION`, `production_ready=false`, `signature_trust=AD_HOC_ONLY`, `notarized=false`.

No Apple payment, Developer ID certificate, Windows provider, production signing cutover, or Software Catalog policy activation is performed by this workflow.
