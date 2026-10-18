# Release policy

This public repository distributes only explicitly approved, certified executable distribution artifacts from reviewed source commits, not source mirrors or private draft metadata.

## Independent products and immutable tags

- Runner V2: `runtime-v2-<version>` (unchanged).
- Shared UAP Browser Extension: `browser-extension-v<version>`; artifact `uap-browser-extension-<version>.zip`, `.sha256`, sanitized provenance.
- UAP Device Control Remote: `device-control-remote-v<version>`; artifact `uap-device-control-remote-<version>.mjs`, `.sha256`, sanitized provenance. Requires separately installed compatible Node.js 26; do **not** call it a standalone native binary.
- Existing Password Manager browser-extension release `v0.8.0` must not be repurposed, overwritten or confused with the shared extension.

Never overwrite an existing release tag or asset, even for a rebuilt artifact. Each source and release version must be checked for uniqueness.

## Release preflight (required)

1. Identify the **exact 40-character source commit SHA**, product version and selected platform/browser targets. A source candidate must have a successful relevant verification/certification run on that exact SHA. The review includes real supported browser pairing and filesystem/browser security checks for these two products; deterministic source tests alone do not establish end-to-end certification.
2. Build candidate artifacts from the reviewed private source. Verify a clean source/manifest, expected artifact allowlist, exact SHA-256 bytes, associated version and checksums. Require sanitized provenance with source SHA, product, version, asset hashes and certification evidence ID. Inspect distribution contents for credentials, tokens, internal machine details, unapproved source material and unintended dependency payloads.
3. For the shared MV3 extension: certify the actual ZIP installed unpacked in supported Chrome/Edge and its optional loopback pairing; verify permissions and disclosed packaged JavaScript. The ZIP necessarily contains inspectable client-side JS and must have a documented disclosure/security review.
4. For the Node Remote: certify the actual bundled `.mjs` entrypoint with the documented Node.js version on intended OSes, explicit roots, OAuth/device pairing, reconnect, and browser companion behavior. Do not imply the `.mjs` embeds Node.js or is code-signed.
5. Native Windows/macOS installers remain separately subject to valid installer signatures. macOS Runner test-only artifacts are not publishable. No JS artifact waives native-installer policy.
6. **Release description is part of the deliverable**: use [release-note templates](RELEASE_NOTES_TEMPLATE.md) and embed complete platform-appropriate download, checksum, installation, pairing, verification and update/rollback instructions in the GitHub Release body. Include the versioned guide links and list exactly the attached assets.
7. Obtain separate explicit publication approval after review and source/asset certification. Publish only allowlisted assets, checksums, sanitized provenance, and the reviewed release body. Never expose private source repositories, logs, CI artifacts, secrets, environment identifiers or private draft notes wholesale.
8. Verify public links **unauthenticated**, download each published asset and rehash the bytes. Record actual URL, SHA-256 and exact source commit after publication. A draft or private CI artifact is not a public release.

Runner V2 publication still requires a successful native certification on exact source SHA, platform-specific signed installer and checksum, and native-ready record. Its older [Runner-specific constraints](https://github.com/CodingFrees/uap-downloads/releases) remain in force; these new product namespaces do not loosen them.
