# Release policy

This public repository distributes only explicitly approved binary artifacts from privately certified source repositories.

Runner V2 uses tags `runtime-v2-<version>`; another product's existing tag is never reused. Candidate releases in the private source repository remain draft and are not public download URLs.

## Preconditions

Before a Runner V2 public release: validate a successful native certification run on the exact 40-character source SHA on `main`, selected-platform evidence, the native-ready record, the canonical manifest and a platform-specific installer and SHA-256 sidecar for each selected platform. Verify the bytes against their sidecars, verify provenance, and reject any unexpected asset or metadata. Verify required platform signatures on the actual installer. Windows and macOS publication must fail closed when signing is absent or invalid. macOS is currently test-only and cannot be published.

Publication requires a separate explicit authorization. The public manifest must include only release version, exact source SHA, certification run ID, artifact names, platforms, architectures and hashes. No private repository snapshot, token, logs, CI artifacts, machine identifiers, environment details or private release notes are mirrored. Never overwrite an existing public release tag or asset. Public distribution is complete only after unauthenticated downloads resolve and digest verification succeeds.

The private source repository remains private regardless of public asset availability.
