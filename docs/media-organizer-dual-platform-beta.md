# BKE Media Organizer — Windows + macOS beta distribution checkpoint

**Intent:** extend the existing PREPRODUCTION-only, exact-artifact Software Catalog publisher to distribute BOTH existing platform packages from one certified BKE Metadata Manager source/run. No Windows Authenticode signing, Apple Developer ID, notarization, production activation, re-build, or release overwrite.

## Pinned evidence — November 9, 2026

- Product source: `jan2xo/bke-metadata-manager@363db36a56fe0a19b942eb783124f3b8ed314419` in draft PR #2.
- Product CI: GitHub Actions run `42181080912` attempt `1`: PASS, all five Windows/Linux/macOS build/test/package jobs.
- macOS artifact `13485089192`, `BKE-Media-Organizer-macOS-ARM64`, outer ZIP SHA-256 `56740d23f2d79e3f3394dcb5e038d1d0b65a2e9ac4ad4d1f3a0f969bddba60f5`.
- Windows artifact `13485486832`, `media-organizer-win-x64`, outer ZIP SHA-256 `de6009f149c941f4616716f3b1353a44b636359a35165f677370a3bf739e40f3`.
- Windows ZIP independently downloaded and hash-verified. It contains `Bke.MetadataManager.exe`, `Bke.MetadataManager.dll`, `Bke.MetadataManager.runtimeconfig.json`, `coreclr.dll`, and the Avalonia dependencies. It is a portable self-contained ZIP, NOT a Windows Installer/MSIX and NOT Authenticode signed.
- macOS built .app is ad-hoc signed and not notarized. Mac and Windows are separate desktop UIs (native SwiftUI vs Avalonia) using the same .NET `MediaOrganizer` core.

## Cross-platform code conflict assessment

No source/merge conflict reported: draft product PR is mergeable, exact candidate CI matrix PASS. The macOS SwiftUI frontend calls the same .NET mover via `--organize-json`, while Windows invokes `MediaOrganizer.MoveAsync` directly. Both share the safe staging/hash/collision refusal behavior. **Feature parity gap:** Windows Avalonia UI has category-add but does not have macOS's remove-category interaction and adaptive SwiftUI tile layout. Windows functionality is not claimed to match the latest Mac-specific redesign. Native GUI acceptance on a real Windows machine is unverified.

## Minimum complete certification graph

- Required: focused Catalog publication trust/provenance review and cheap exact-head PR Guard covering both macOS and Windows exact-artifact manifest/zip intake; no automatic publication.
- Reused cross-repo proof: already green exact-source BKE Metadata Manager build and test run 42181080912; no product rebuild or CI retrigger.
- Not required: Agent, Digital Solutions, UTM, Apple notary, Windows trusted signing, unrelated product runtime suites.
- Publication gate: separate owner-only explicit `workflow_dispatch` on Catalog main, protected cross-repository read-only `MEDIA_ORGANIZER_ARTIFACT_READ_TOKEN`, no existing release/tag, **preproduction only**.
- Release assets: macOS original DMG and ZIP, original Windows ZIP (renamed for predictable consumer label but exact archive bytes), SHA-256 manifest; no packaging modification to the original Windows archive.
- The signed/published release, platform-specific GUI interactions and production-readiness may not be claimed until separately verified.

Production locked. No publication during PR implementation or merge.