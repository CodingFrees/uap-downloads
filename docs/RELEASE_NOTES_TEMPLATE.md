# GitHub Release body templates

Copy the **appropriate entire section** into the GitHub Release description and fill every `REPLACE_*` value from verified release evidence. Do not publish unresolved placeholders. This is **required** installation documentation in each release body, in addition to the versioned guides.

## Shared UAP Browser Extension

**Title:** UAP Browser Extension REPLACE_VERSION  
**Tag:** `browser-extension-vREPLACE_VERSION`  
**Certified source SHA:** `REPLACE_40_CHAR_SHA`  
**Certification evidence:** `REPLACE_RUN_ID`  
**Supported browsers:** `REPLACE_CERTIFIED_CHROME_EDGE_VERSIONS`

**Assets attached**
- `uap-browser-extension-REPLACE_VERSION.zip`
- `uap-browser-extension-REPLACE_VERSION.zip.sha256`
- `uap-browser-extension-REPLACE_VERSION.provenance.json`

**Install — Chrome / Edge**

1. Download the ZIP and matching `.sha256` file from this release's **Assets**.
2. Validate SHA-256: Windows PowerShell `(Get-FileHash .\uap-browser-extension-REPLACE_VERSION.zip -Algorithm SHA256).Hash`; Linux `sha256sum uap-browser-extension-REPLACE_VERSION.zip`; macOS `shasum -a 256 uap-browser-extension-REPLACE_VERSION.zip`. Compare the full digest with the sidecar.
3. Extract to a **persistent** directory with `manifest.json` directly inside.
4. Open Chrome `chrome://extensions` or Edge `edge://extensions`, enable **Developer mode**, click **Load unpacked**, and choose the extracted directory.
5. Verify **UAP Browser Extension** is installed; configure/authorize the intended UAP connection as applicable.

**Pair with Device Control (optional)**

Start your authorized Device Control Remote. In the extension popup select **Device Control · Browser**, enter the short-lived pairing code and port reported by Remote (normally `18700`), and enable browser control. The optional UAP `device-control-browser` companion must be installed and authorized. The extension's installation alone does not grant device/browser access.

**Update/removal**

Verify a new approved ZIP, replace/reload the unpacked extension in the browser, and check whether browser pairing needs repeating. To revoke access, remove the extension and revoke device pairing in UAP; stopping the UI alone does not revoke credentials. Troubleshooting and full instructions: [Chrome/Edge installation](https://github.com/CodingFrees/uap-downloads/blob/browser-extension-vREPLACE_VERSION/docs/INSTALL_BROWSER_EXTENSION.md).

**SHA-256 for ZIP:** `REPLACE_64_HEX_DIGEST`. This is an unpacked developer-mode extension distribution, **not** a Chrome/Edge store listing. The packaged client JS is inspectable.

## UAP Device Control Remote

**Title:** UAP Device Control Remote REPLACE_VERSION  
**Tag:** `device-control-remote-vREPLACE_VERSION`  
**Certified source SHA:** `REPLACE_40_CHAR_SHA`  
**Certification evidence:** `REPLACE_RUN_ID`  
**Certified OSes:** `REPLACE_VERIFIED_WINDOWS_LINUX_MACOS`

**Assets attached**
- `uap-device-control-remote-REPLACE_VERSION.mjs`
- `uap-device-control-remote-REPLACE_VERSION.mjs.sha256`
- `uap-device-control-remote-REPLACE_VERSION.provenance.json`

**Install — Windows / Linux / macOS**

1. Install **Node.js >=26.8.1 and <27** and verify `node --version`. This portable JavaScript file is **not** a signed native installer and does not include Node.js.
2. Download this release's `.mjs` and corresponding `.sha256`, then compare SHA-256. PowerShell: `(Get-FileHash .\uap-device-control-remote-REPLACE_VERSION.mjs -Algorithm SHA256).Hash`; Linux: `sha256sum uap-device-control-remote-REPLACE_VERSION.mjs`; macOS: `shasum -a 256 uap-device-control-remote-REPLACE_VERSION.mjs`.
3. Obtain a short-lived pairing code from the intended UAP Device Control admin console. Run in a terminal, replacing URL/code/path:
   ```sh
   node /path/to/uap-device-control-remote-REPLACE_VERSION.mjs login --origin https://YOUR-UAP-ORIGIN --pairing-code YOUR-ONE-TIME-CODE
   node /path/to/uap-device-control-remote-REPLACE_VERSION.mjs status
   node /path/to/uap-device-control-remote-REPLACE_VERSION.mjs remote --read-only-root files=/absolute/approved/directory
   ```
   In Windows PowerShell replace the program path with a Windows path and quote the root parameter, e.g. `--read-only-root "files=C:\Approved\Documents"`.
4. Keep the Remote running while control is needed; press Ctrl+C to stop. Without explicit root options, the client exposes the **current working directory**, so select that directory carefully.

**Pair browser extension (optional)**

Download the independent shared **UAP Browser Extension** release, then enter Remote's one-time bridge code/port in **Device Control · Browser** in its popup; grant permissions explicitly. Default loopback port is `18700`. For file/process-only mode, use `remote --no-browser-control`.

**Update/removal**

Stop the old Remote, verify and start the new `.mjs`, then confirm `status`. Keep the previous approved file as manual fallback. `logout` and UAP device revocation are necessary to end authorization; deleting `.mjs` alone does not revoke it. Do not install a redundant persistent client on a machine already running Runner V2. Full instructions: [Windows/Linux/macOS installation](https://github.com/CodingFrees/uap-downloads/blob/device-control-remote-vREPLACE_VERSION/docs/INSTALL_DEVICE_CONTROL_REMOTE.md).

**SHA-256 for MJS:** `REPLACE_64_HEX_DIGEST`. The independent existing npm distribution is `@codingfrees/uap-device-control`; npm availability is not proof of a GitHub release.

---

**Maintainer gate:** verify the release version/tag, exact source SHA, certification ID, all asset names/checksums and unauthenticated public download; exclude all private machine, CI, user and credential data. Require explicit publication authorization and never reuse an existing tag.
