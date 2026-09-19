# UAP Downloads

This public repository distributes approved binaries only. The UAP and Local Node Runner V2 source repositories, private certification records and draft releases stay private.

## Available products

- **Password Manager browser extension:** existing release `v0.8.0` is independent and remains unchanged.
- **Local Node Runner V2:** approved releases use the separate `runtime-v2-<version>` tag namespace. See [all releases](https://github.com/CodingFrees/uap-downloads/releases). A Runner download is available only when the matching public release and installer asset exist; no private draft URLs are public downloads.

Each published Runner installer must include a matching `.sha256` sidecar and a sanitized `native-installers-manifest.json` recording the exact certified source SHA and provenance. Linux (`.deb`) and Windows (signed `.exe`) can be published only when individually certified and approved. macOS remains test-only until native certification and trusted signing are complete.

Verify the downloaded installer checksum before installation. See the [release policy](docs/RELEASE_POLICY.md). Never commit private source, secrets or installer binaries into this repository.
