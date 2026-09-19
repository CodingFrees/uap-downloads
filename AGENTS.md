# Public downloads repository

This repository distributes approved release assets only; it is not a source-code mirror.

- Keep private `CodingFrees/local-node-runner-v2` and `CodingFrees/universal-agent-platform` source, commits, logs, credentials and CI artifacts private.
- Publish only explicitly approved and certified binary artifacts, SHA-256 checksum sidecars and a sanitized manifest/provenance statement. Never mirror private release metadata wholesale.
- Preserve independent product tag namespaces; `runtime-v2-*` is reserved for Runner V2. Do not alter existing Password Manager releases.
- Never publish an unsigned Windows/macOS installer or a macOS test-only artifact. Any missing certification, source SHA, expected digest or signature must fail closed.
- Preserve immutable release tags; refuse an existing conflicting tag instead of overwriting assets.
- Public download links must resolve without GitHub authentication and match advertised SHA-256 before being presented in UAP.
- Changes follow branch → pull request → evidence → explicitly approved merge/publication; no automatic publication of a private draft.
