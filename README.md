# UAP Downloads

Public distribution of **approved, certified release artifacts**. Source repositories, private certification logs, and draft builds stay private. A file named in the documentation is **not downloadable until its matching public release and asset exist**.

## Products and installation

| Product | Release tags | Installation |
| --- | --- | --- |
| **UAP Browser Extension** (shared Chrome/Edge MV3 extension, with optional Device Control browser companion) | `browser-extension-v<version>` | [Chrome/Edge install and browser pairing](docs/INSTALL_BROWSER_EXTENSION.md) |
| **UAP Device Control Remote** (portable Node.js outbound client) | `device-control-remote-v<version>` | [Windows, Linux and macOS install](docs/INSTALL_DEVICE_CONTROL_REMOTE.md) |
| **Password Manager Browser Extension** (legacy independent release `v0.8.0`) | Existing `v*` tag | Existing release is unchanged; do not confuse it with the shared UAP Browser Extension |
| **Local Node Runner V2** | `runtime-v2-<version>` | Approved native installer assets when available; distinct from temporary Device Control Remote |

Browse [all public releases](https://github.com/CodingFrees/uap-downloads/releases). Use a release's attached SHA-256 file to verify the downloaded asset before installing/running it.

**Important:** The shared extension and Device Control Remote are **planned public distribution channels** until their dedicated releases are explicitly approved, certified, and published. The Node Remote client also has an independent npm distribution (`@codingfrees/uap-device-control`); availability on npm does not establish that a GitHub release exists.

## Release documentation requirement

Every shared extension or Remote release **must include product-specific, copy-ready installation and pairing instructions in its GitHub Release description**, not merely a link to a README. The release body also links the corresponding detailed installation guide and identifies supported browser/OS, prerequisites, version, asset names, checksum and verified source SHA.

Release maintainers use [release-description templates](docs/RELEASE_NOTES_TEMPLATE.md) and [release policy](docs/RELEASE_POLICY.md). Private draft assets are not public download URLs.
