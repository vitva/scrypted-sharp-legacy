# Scrypted Sharp Legacy (x86-64)

A compatibility build of **Sharp 0.34.5** and **libvips 8.17.3** for older x86-64 Linux CPUs that do not support AVX.

The project was created to make the Sharp image-processing dependency usable by the Scrypted Snapshot Plugin on legacy hardware.

## Why this exists

Recent prebuilt Sharp/libvips binaries may execute CPU instructions that are unavailable on older processors, causing an `Illegal instruction` (`SIGILL`) crash.

This workflow builds libvips and Sharp from source with a baseline x86-64 target:

- `-march=x86-64`
- `-mtune=generic`
- libvips Highway and ORC optimizations disabled

## Build versions

| Component | Version |
| --- | --- |
| Sharp | 0.34.5 |
| libvips | 8.17.3 |
| Build environment | Ubuntu 24.04 |
| Target | Linux x86-64 baseline |

## Download a release

The recommended download is the permanent GitHub Release:

- **Latest release:** [Scrypted Sharp Legacy v1.0.0](https://github.com/vitva/scrypted-sharp-legacy/releases/tag/v1.0.0)
- **Archive:** `sharp-legacy-x86_64.tar.gz`

Tagged builds (`v*`) are published automatically as GitHub Releases. The release archive remains available independently of the temporary Actions artifacts.

## Build artifact

The GitHub Actions workflow also uploads an artifact named **`sharp-legacy-x86_64`**.

To obtain this temporary build artifact:

1. Open the **Actions** tab in this repository.
2. Select the relevant successful **Build legacy x86-64 Sharp** run.
3. Download the `sharp-legacy-x86_64` artifact.

Actions artifacts are temporary and currently retained for 14 days; use the GitHub Release for a permanent download.

## Compatibility and testing

The resulting build was tested on an AMD G-T56N (Bobcat) system without AVX support. Sharp successfully generated JPEG, PNG, and WebP images on that machine.

This is a hardware-specific compatibility project, not an official Sharp, libvips, or Scrypted release.

## Important notes

- Intended for Linux x86-64 systems with older CPUs lacking AVX.
- The archive includes Sharp and the custom libvips libraries; runtime library dependencies must also be available on the target system.
- This build disables some optional libvips features and is not intended to provide every codec or optimization available in a standard build.
- Back up the existing Sharp package and libraries before replacing anything in a working Scrypted installation.
- Test snapshots and notifications with your own cameras after installation.

## License

Sharp and libvips are third-party projects with their own licenses. This repository contains build automation and packaging instructions; consult the upstream projects for their license terms.
