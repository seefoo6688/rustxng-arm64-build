# RustXNG Linux ARM64 build

This isolated repository contains the build workflow and its documentation only. It builds the official RustXNG source at commit `08338038491d57adcfa4990ddf3d8925af292f4e` on a native GitHub-hosted Linux ARM64 runner, using the locked Cargo dependency set and Rust 1.99.1. It runs the upstream offline smoke test and publishes the binary with its SHA-256 checksum, source commit, build metadata, and license files.

## Security boundaries

- The workflow grants the repository token `contents: read` only. All referenced GitHub Actions are pinned to full commit SHAs; the pinned commits were checked against their official repositories and have valid GitHub commit signatures.
- Checkout credentials are not persisted. The workflow has no configured secrets, deployment credentials, or connection to a production host; it only builds and uploads a GitHub Actions artifact.
- The artifact checksum detects accidental or in-transit changes relative to that build. It is not a maintainer signature, so verify its source commit and checksum before installation.
- The artifact is retained for seven days and contains the executable, checksum, source commit, licenses, and non-secret build metadata.

## Build and install

Commit these three files to `main` to start the build, or use **Actions → Build RustXNG Linux ARM64 → Run workflow**. Download the `rustxng-linux-arm64` artifact after the workflow and smoke test succeed.

On the ARM64 host, the project's separate local installer verifies the checksum, pinned source commit, executable architecture, host glibc, and version before staging the binary. Installation does not start RustXNG or change the active search route. Run it temporarily as an unprivileged user on loopback with resource limits, then compare live results and resource use before any production route change.
