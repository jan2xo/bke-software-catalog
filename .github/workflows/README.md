# Active GitHub Actions

This repository keeps publication intentional and separate from ordinary CI.

Active workflows:

- `pr-guard.yml` — cheap automatic pull-request policy guard only. It never publishes a release.
- `publish-agent-preproduction.yml` — explicit `workflow_dispatch` entrypoint for BKE Licensing Agent PREPRODUCTION publication.

The prior Agent 0.x/1.x publication workflows remain preserved verbatim under
`.github/legacy-workflows/2026-10-02/`.

## Agent PREPRODUCTION publication contract

The active publication workflow:

- consumes an already-certified `agent-installer-package` from
  `jan2xo/bke-licensing-agent`;
- pins the exact Agent source SHA, certification run ID, artifact ID, version,
  installer SHA-256, and byte count;
- requires the Agent installer certification and aggregate required-certification
  jobs to have passed for that exact source SHA;
- verifies the immutable `bke.agent-installer-package.v2` manifest before
  publication;
- never clones, builds, compiles, or repackages Agent source;
- uses `AGENT_ARTIFACT_READ_TOKEN` only to read the exact cross-repository
  certified Actions artifact;
- requires the explicit `PUBLISH_AGENT_PREPRODUCTION` authorization input;
- refuses to overwrite an existing release or tag;
- creates a GitHub prerelease with `production_ready=false`;
- does not make the PREPRODUCTION release the repository's latest release; and
- re-downloads the published installer and verifies its SHA-256 and byte count.

Merging the workflow does **not** publish an Agent release. Publication remains a
separate explicit intent and must use the final trust-bearing certified installer.

Production remains locked.
