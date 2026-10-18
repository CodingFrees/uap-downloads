# Public downloads repository

This repository distributes approved release artifacts only; it is not a source-code mirror.

- Keep private `CodingFrees/local-node-runner-v2` and UAP source, private CI logs, credentials, and drafts private.
- Public release artifacts may be individually reviewed browser-extension ZIPs and bundled Node.js CLI executable entrypoints (`.mjs`), in addition to certified native installers. Browser JS distributed to end users is inherently inspectable: require an explicit source-disclosure/security review before publication; never copy an unrelated private source tree or development files.
- Publish only explicitly approved, certified release artifacts with SHA-256 checksum sidecars and sanitized manifest/provenance. Never mirror private CI metadata wholesale.
- Keep product tag namespaces independent: `runtime-v2-*` is for Runner V2, `browser-extension-v*` for the shared extension, and `device-control-remote-v*` for the outbound Node client. Do not alter the existing Password Manager release.
- Never publish an unsigned Windows/macOS native installer or a macOS test-only native artifact. Do not misrepresent portable JavaScript as a signed native executable.
- Missing certification, exact source SHA, expected digest, required security review, or applicable signature must fail closed.
- Preserve immutable release tags and assets; refuse a conflicting existing tag.
- Public download links must resolve without authentication and match their published SHA-256. The release body must contain complete installation instructions for its product and link its versioned assets.
- Follow branch → pull request → evidence → explicitly approved merge/publication. No automatic publication of private drafts.
