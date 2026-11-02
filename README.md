# Contrast 21 - Accessible Color Checker

Contrast 21 helps you choose foreground and background colors that work together
and meet WCAG contrast requirements. Sample and refine colors, explore accessible
palettes, and keep your own color collections nearby. A unique feature
is a color swath generator that previews colors with your brand colors, and
snaps to contrast safe colors.

Built with React and Tauri, it runs as a browser interface or a desktop app.
Your saved colors stay on your device; no account or server is required.

## Keyboard shortcuts

Hold **Ctrl** to show the key for each available shortcut beside its label.
Press **Ctrl+Shift** with that key to use it. Shortcuts are off while the
eyedropper is active. While the color refinement panel is open, Tab stays inside
it until you close it with Escape or click outside it. Only the foreground and
background shortcuts work at that time.

In the Grid panel and the color refinement panel's web colors, the arrow keys
move between swatches, Home and End jump to the start or end of a row, and
Ctrl+Home or Ctrl+End jump to the first or last swatch. The refinement sliders
change by one step with the arrow keys.

| Shortcut | Action |
| --- | --- |
| Ctrl+Shift+P | Open the Pick panel and focus the start of Live preview |
| Ctrl+Shift+H | Open the Harmony panel |
| Ctrl+Shift+G | Open the Grid panel and focus its current-pair cell |
| Ctrl+Shift+M | Open the My Colors panel |
| Ctrl+Shift+F | Select the foreground color |
| Ctrl+Shift+B | Select the background color |

## Run the interface

Use Node.js 22.20 or newer. With [nvm](https://github.com/nvm-sh/nvm), use the
project's pinned version:

```bash
nvm install
nvm use
npm ci
npm run dev
```

Open http://127.0.0.1:1420. Run `npm test` to check the tests.

For the desktop app, install the [Tauri prerequisites](https://v2.tauri.app/start/prerequisites/)
and run `npm run tauri -- dev`.

## Build

**Browser interface**

```bash
npm run build
```

The output is in `dist/`. Use `npm run preview` to try the built interface locally.

**Windows MSIX**

The [Windows MSIX workflow](./.github/workflows/msix-latest.yml) builds on pushes
to `main`. Download **Contrast21-msix** from a successful run's **Artifacts**
section. Pushed `v*` tags also publish a GitHub Release when the tagged commit is
in `main` history and its version matches the app.

For a local build from Ubuntu/WSL, install Rust, MinGW, and wixl, then run:

```bash
npm run build:windows
npm run package:msix
```

MSIX packaging requires Windows PowerShell through WSL. On Windows, you can run
[scripts/package-msix.ps1](./scripts/package-msix.ps1) directly with `-SourceDir`
pointing to a built app and `-SourceTarget x86_64-pc-windows-msvc` for a native
MSVC build.

Packages use the Store identity in [identity.json](./identity.json) and are written
to `releases/msix/<version>/` (`releases/msix/latest/` on the CI runner).
The MSIX filename is always `Contrast21_windows_x64.msix`, and the Actions download
is `Contrast21-msix.zip`, including for tagged builds. Neither filename includes
`latest` or a version. The package version remains in the MSIX manifest and
`release.json`; the sideload certificate is named `Contrast21_sideload.cer`.
For sideload installation, extract the package files together and run
`Install-Contrast21.cmd`. Microsoft Edge WebView2 must already be installed.
These builds use self-signed sideload certificates, not Public Trust signing;
the [signed Windows release guide](./docs/windows-signed-releases.md) covers that
separate workflow.

### Update the Microsoft Store listing

Git tags do not change app or package versions, and GitHub Releases do not
automatically update Partner Center.

1. Increase the version in `package.json`, `src-tauri/tauri.conf.json`, and
   `src-tauri/Cargo.toml` together, and synchronize both lockfiles. Update the
   defaults in `scripts/package-msix.sh` and `scripts/package-msix.ps1` to the
   corresponding four-part MSIX version when packaging locally.
2. Commit and push the changes to `main`, then create and push a matching `v*`
   tag. For app version `1.3.7`, use tag `v1.3.7`; the workflow builds MSIX
   version `1.3.7.0`. Do not move an existing release tag.
3. Wait for the tagged **Windows MSIX build** to succeed. Download its
   **Contrast21-msix** artifact or the MSIX from the corresponding GitHub Release.
4. In Partner Center, create or edit the app's submission and upload
   `Contrast21_windows_x64.msix`. Verify that the displayed package version is
   `1.3.7.0`, complete any capability declarations (including `runFullTrust`),
   and submit the update for certification and publication.

The package uses the reserved Store identity. Its self-signed certificate is for
sideload testing; Microsoft signs packages distributed through the Store.
The separate Public Trust signing workflow is not required for this MSIX Store
submission. Do not upload the `.cer`, installer script, or whole artifact ZIP.
Every changed Store package needs a new, higher manifest version; renaming the
file or rebuilding the same version does not resolve a package identity conflict.

**Linux desktop**

With Rust and the Tauri system dependencies installed:

```bash
npm run tauri -- build --config src-tauri/tauri.linux.conf.json
```

The Debian package is written under `src-tauri/target/release/bundle/deb/`.
