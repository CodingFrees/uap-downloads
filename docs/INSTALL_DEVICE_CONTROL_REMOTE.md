# UAP Device Control Remote — Windows, Linux, macOS

This is the **outbound Node.js client** (`@codingfrees/uap-device-control`), not Runner V2 and not the separate persistent Device Agent. It provides scoped file/process capabilities and, with the shared browser extension, optional semantic browser control. It does **not** require opening an inbound Internet port.

## Requirements and authorization

- Supported runtime in source: **Node.js 26.x, at least 26.8.1 and below 27**. Check with `node --version`. The portable `.mjs` asset does **not** bundle Node.js.
- An authorized UAP Device Control HTTPS origin with OAuth/remote-device routes, a workspace/device identity and a **short-lived admin-issued pairing code** from the UAP Device Control admin console. Do not assume that the publicly available development endpoint is your production origin.
- Local directory roots intentionally chosen by the user. Without `--root` arguments, `remote` exposes **the current working directory** as the default root. Run from an explicitly chosen directory, not from the whole system drive/home folder.

## Option A — direct download from UAP Downloads

Use this method **only once** a public `device-control-remote-v<version>` release actually contains the approved `uap-device-control-remote-<version>.mjs` asset and its checksum.

1. Download the versioned `.mjs` and matching `.mjs.sha256` from [UAP Downloads Releases](https://github.com/CodingFrees/uap-downloads/releases). Save them together in a stable directory.
2. Compare SHA-256 against the complete sidecar value. **Windows PowerShell:** `(Get-FileHash .\uap-device-control-remote-<version>.mjs -Algorithm SHA256).Hash`. **Linux:** `sha256sum uap-device-control-remote-<version>.mjs`. **macOS:** `shasum -a 256 uap-device-control-remote-<version>.mjs`.
3. Open a terminal in a deliberately scoped working directory and run, replacing `<version>`, the HTTPS origin and one-time code:
   ```sh
   node /path/to/uap-device-control-remote-<version>.mjs login --origin https://YOUR-UAP-ORIGIN --pairing-code YOUR-ONE-TIME-CODE
   node /path/to/uap-device-control-remote-<version>.mjs status
   node /path/to/uap-device-control-remote-<version>.mjs remote --read-only-root files=/absolute/approved/directory
   ```
   In Windows PowerShell use a Windows path to the `.mjs` file and a quoted root argument, e.g. `--read-only-root "files=C:\Approved\Documents"`. Use `--root` only when write access is intended.
4. Leave the Remote process running while you need temporary device/browser control. Stop it with **Ctrl+C**. The actual origin and granted roots should be reviewed locally before starting.

## Option B — existing npm distribution

With compatible Node.js/npm installed, no GitHub ZIP is required:
```sh
npx @codingfrees/uap-device-control@latest login --origin https://YOUR-UAP-ORIGIN --pairing-code YOUR-ONE-TIME-CODE
npx @codingfrees/uap-device-control@latest status
npx @codingfrees/uap-device-control@latest remote --read-only-root files=/absolute/approved/directory
```
npm versions and GitHub release tags have **separate** availability; verify the npm package version before using `latest` in a reproducible setup.

## Optional browser extension

The Remote process normally opens a local-only semantic browser bridge on `127.0.0.1:18700` and prints a short-lived pairing code. Install the [shared browser extension](INSTALL_BROWSER_EXTENSION.md), open its **Device Control · Browser** UI, enter the displayed code/port and explicitly enable browser control. To run only file/process control, pass `--no-browser-control` to `remote`. If port `18700` conflicts, start with `--browser-port PORT` and pair to that reported port.

Browser control works through the extension, not through remote-debugging flags; it only exposes capabilities actually authorized by the provider, user permissions and UAP workspace policy.

## Persistent use, update and removal

- `install-service` is an **optional** persistence mode after login, using the platform's existing service adapter. It is not required for temporary `remote` and must not be installed to duplicate an existing Runner V2 host. Its lifecycle is separate from GitHub/npm downloads and does **not** imply signed automatic updates.
- For a new public `.mjs` version: stop the existing Remote, verify the new checksum, launch the new file with the existing authorized state/origin after checking release compatibility, then confirm `status`. Retain the previously approved file until successful verification; do not publish or copy local authentication state.
- If browser bridge pairing was lost: stop `remote`, run `node /path/to/uap-device-control-remote-<version>.mjs browser-reset` (or the npm equivalent), restart Remote and pair the extension again.
- `logout` revokes/clears the client's authenticated state; also revoke the device/permissions in UAP when decommissioning the machine. Simply deleting the downloaded file does not revoke server-side authorization.
- WSL/Linux controls the WSL/Linux filesystem and capabilities, **not native Windows desktop input**. For native Windows behavior run the approved client on Windows. The installed Runner V2 is a separate, preferable production path when already present.

Never disclose UAP tokens, one-time pairing codes, local credentials, private filesystem paths or machine configuration in public release notes or support logs.
