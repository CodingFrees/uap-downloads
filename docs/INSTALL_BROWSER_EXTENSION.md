# UAP Browser Extension — Chrome and Microsoft Edge

These instructions apply to the **shared UAP Browser Extension**, not the separate Password Manager `v0.8.0` download. A public versioned ZIP is available only after the `browser-extension-v<version>` release has been approved and published.

## Install from an approved release

1. Open [UAP Downloads Releases](https://github.com/CodingFrees/uap-downloads/releases) and choose the correct **UAP Browser Extension** release. Download `uap-browser-extension-<version>.zip` and its matching `.zip.sha256` sidecar. Do not use a private draft or unrelated Password Manager ZIP.
2. Verify the ZIP's SHA-256 matches the sidecar. Windows PowerShell: `(Get-FileHash .\uap-browser-extension-<version>.zip -Algorithm SHA256).Hash`; Linux: `sha256sum uap-browser-extension-<version>.zip`; macOS: `shasum -a 256 uap-browser-extension-<version>.zip`. Compare all 64 hexadecimal characters, not just a prefix.
3. Extract the ZIP to a dedicated **persistent** directory. The selected extension directory must contain `manifest.json` directly (not another nested ZIP directory). Do not delete or move the extracted files while the extension is installed.
4. Chrome: open `chrome://extensions`; Edge: open `edge://extensions`. Enable **Developer mode**, select **Load unpacked**, and select the directory containing `manifest.json`.
5. Confirm the extension is named **UAP Browser Extension** and inspect the requested permissions. Configure its intended UAP origin/workspace through the extension UI as applicable. Normal authenticated UAP access is required; installing the extension does not authorize Device Control automatically.

**Security:** Developer-mode unpacked installation is not a Chrome Web Store or Microsoft Edge Add-ons publication. Install only the ZIP verified from the approved release. Client-side extension code is inspectable. Do not grant browser/site permissions that you do not intend to use.

## Optional browser control pairing with UAP Device Control Remote

1. Install and start the Node client using the [Remote installation guide](INSTALL_DEVICE_CONTROL_REMOTE.md), and confirm its outbound Device Control connection.
2. Ensure the UAP workspace has authorized Device Control and its optional `device-control-browser` companion; the Remote CLI should announce a local browser bridge, normally at `127.0.0.1:18700`, and a short-lived pairing code.
3. Open the extension popup → **Device Control · Browser**. Enter the **code and port displayed locally by the CLI**, pair, and explicitly enable browser control.
4. Check that Remote reports extension connected and the authorized UAP Device Control surface advertises the available browser tools. A working extension alone does not imply authorization or active connection.

The bridge accepts loopback connections only. Browser tools use explicit consent/approval and do not require Chrome/Edge remote-debugging flags. Browser control includes authorized tabs/navigation/page snapshots/selector interactions, not unrestricted background desktop input.

## Update, disconnect, troubleshoot

- For a new approved ZIP, verify its checksum, extract to a stable location, then update/reload the unpacked extension via the browser extension page. Depending on extension identity/storage continuity, pairing may need to be completed again; do not copy credentials manually.
- If Remote reports pairing stored but extension offline, open the extension settings' **Device Control · Browser → Reconnect browser bridge** and confirm the actual CLI-reported port; older saved installations may still point to `8800` whereas new Remote defaults to `18700`.
- If pairing identity was lost: stop Remote, invoke its `browser-reset` command, restart Remote and pair again using its new one-time code. Browser reset preserves the device login; never post a pairing code publicly.
- If browser capabilities are missing, verify the optional workspace companion is installed/authorized, the extension has needed browser permissions, the Node client is running on the intended host OS, and the browser bridge has connected.
- To remove: disable/remove the extension in Chrome/Edge and revoke the corresponding UAP/Remote pairing as appropriate. Merely closing the popup is not revocation.
