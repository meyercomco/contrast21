# Contrast 21 - Accessible Color Checker

Contrast 21 helps you choose foreground and background colors that work together
and meet WCAG contrast requirements. Sample and refine colors, explore accessible
palettes, and keep your own color collections nearby. A unique feature
is a color swath generator that previews colors with your brand colors, and
snaps to contrast safe colors.

Built with React and Tauri, it runs as a browser interface or a desktop app.
Your saved colors stay on your device; no account or server is required.

## Import My Colors

In **My Colors**, enter one `color name: #hex` per line, then select **Import**:

```text
Primary Blue: #005A9C
Ink: #1C1917
Copper: #B86A32
```

Names may contain spaces. Spaces around names, colons, and color values are
trimmed. You can also paste copied Harmony palette values such as
`--foreground: #F4FCFB;`: the leading `--` and trailing `;` are removed before
saving. Existing pipe-separated lists, bare color values, and JSON imports
remain supported.

## Keyboard shortcuts

Hold **Ctrl** to show the key for each available shortcut beside its label.
Press **Ctrl+Shift** with that key to use it. Shortcuts are off while the
eyedropper is active. While the color refinement panel is open, Tab stays inside
it until you close it with Escape or click outside it. Only the foreground and
background shortcuts work at that time.

In the Grid panel and the color refinement panel's web colors, the arrow keys
move between swatches, Home and End jump to the start or end of a row, and
Ctrl+Home or Ctrl+End jump to the first or last swatch. In the Grid panel,
Ctrl+Shift with an arrow also moves one cell in that direction and previews it.
That shortcut focuses the grid first, so it works when focus is on another control.
The refinement sliders change by one step with the arrow keys.

The Windows app draws a circular magnification lens around the pointer while
sampling. Arrow keys move one pixel, Shift plus an arrow jumps ten, Enter or
click confirms, and Escape or right-click cancels. Close Windows Magnifier if
the lens cannot start.

| Shortcut | Action |
| --- | --- |
| Ctrl+Shift+P | Open the Pick panel and focus the start of Live preview |
| Ctrl+Shift+H | Open the Harmony panel |
| Ctrl+Shift+G | Open the Grid panel and focus its current-pair cell |
| Ctrl+Shift+Arrow | In the Grid panel, focus the grid, move one cell that way, and preview it |
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

`npm run package:msix` uses the version in `package.json`. Pass a version or output
folder when you need a different package identity:

```bash
npm run package:msix -- --version 1.2.3
npm run package:msix -- --tag latest
npm run package:msix -- v1.2.3
```

A version may be `1.2.3`, `1.2.3.0`, or `v1.2.3`. The MSIX package version is the
four-part form, and that is also the default output folder. `--tag` changes only
the folder name. On Windows, pass the same values to
[scripts/package-msix.ps1](./scripts/package-msix.ps1) as `-PackageVersion` and
`-Tag`, with `-SourceDir` pointing to a built app and `-SourceTarget
x86_64-pc-windows-msvc` for a native MSVC build. MSIX packaging requires Windows
PowerShell through WSL.

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

1. Increase the version in `package.json` only. Keep it as `major.minor.patch`.
   `npm version <version> --no-git-tag-version` updates `package.json` and
   `package-lock.json` together. The Tauri config reads that version; packaging
   scripts do not store a default version.
2. Commit and push the changes to `main`, then create and push a matching `v*`
   tag, such as `v` plus the `package.json` version. The workflow builds the MSIX
   version by appending `.0`. Do not move an existing release tag.
3. Wait for the tagged **Windows MSIX build** to succeed. Download its
   **Contrast21-msix** artifact or the MSIX from the corresponding GitHub Release.
4. In Partner Center, create or edit the app's submission and upload
   `Contrast21_windows_x64.msix`. Verify that the displayed package version is
   the `package.json` version plus `.0`, complete any capability declarations
   (including `runFullTrust`), and submit the update for certification and
   publication.

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
