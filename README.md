# Contrast 21 - Accessible Color Checker

Contrast 21 helps you choose foreground and background colors that work together
and meet WCAG contrast requirements. Sample and refine colors, explore accessible
palettes, and export your collections for scss. Contrast 21 also allows you
explore pallets using a color wheel and algorithms , and to snap to contrast
requirements, with your brand colors.

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
sampling. Click to select a color or right-click to cancel. Close Windows
Magnifier if the lens cannot start.

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

## Languages

The interface supports English, Spanish, French, German, Brazilian Portuguese,
Simplified Chinese, Japanese, Korean, Hindi, and Arabic. Arabic uses a
right-to-left layout, including matching color slider direction.

Use **Language** in the tools rail to switch immediately. Languages are listed
in their native names. Your choice is saved on your device. **System default**
follows your browser or system language preferences, including browser language
changes while the app is open. Unsupported languages fall back to English.
Chinese variants use Simplified Chinese; Portuguese variants use Brazilian Portuguese.
Your saved color names remain as you entered them.

### Maintaining translations

The interface is translated with [i18next](https://www.i18next.com/) and
[react-i18next](https://react.i18next.com/). English (`src/locales/en.json`) is the
authoritative source. Each other language has one JSON file in `src/locales/`, with the
same nested keys.

Language choice resolves in this order: a saved explicit selection, then the first
supported entry in the system or browser languages (regional variants match their base
language, so `es-MX` uses Spanish and `pt-PT` uses Brazilian Portuguese), then English.
Users can change the language in the selector in the tab rail.

To add a language:

1. Copy `src/locales/en.json` to `src/locales/<code>.json` and translate every value. Keep
   the keys, `{{placeholders}}`, and `<kbd>` tags unchanged. Plural groups use CLDR
   categories for that language (check them with `new Intl.PluralRules('<code>').resolvedOptions().pluralCategories`).
2. Import it into `dictionaries` in `src/i18n/languages.ts`. Native language names come
   from `Intl.DisplayNames`; i18next handles regional matching and text direction.
3. Run `npm test`. Locale tests check key parity, placeholders, and all required plural forms.

Keep translation keys stable and do not put translated text in internal identifiers,
storage keys, or color data.

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
in `main` history and its version matches the app. A tagged release then runs the
[public sync workflow](./.github/workflows/public-sync.yml), which copies the
public documentation and tags to the public repository.

For a local build from Ubuntu/WSL, install Rust and MinGW, then run:

```bash
npm run package:msix
```

The script builds the Windows EXE and WebView2 loader, then packages them. It
needs Windows PowerShell through WSL. It uses the version in `package.json`.

The Store version is always `major.minor.patch.0`. The last `.0` is required by
Partner Center. It is not another patch. `1.4.1` in `package.json` is already
the patch, and the package is `1.4.1.0`, written to `releases/msix/1.4.1.0/`.
If that package needs a fix, the Store does not expect `1.4.1.1`. Partner Center
rejects a non-zero fourth number, and the packaging script refuses it. Raise the
patch instead: `1.4.2` is packaged as `1.4.2.0`.

Packages use the Store identity in [identity.json](./identity.json). Local output
is `releases/msix/<version>.0/`; CI writes `releases/msix/latest/`. The file is
always `Contrast21_windows_x64.msix`. The Actions download is
`Contrast21-msix.zip`. Sideload builds include a self-signed
`Contrast21_sideload.cer`. Extract the files together and run
`Install-Contrast21.cmd`. Microsoft Edge WebView2 must already be installed.
The Store re-signs accepted packages, so no CA certificate is needed for
submission.

### Update the Microsoft Store listing

Tags and GitHub Releases do not update Partner Center.

1. Raise the patch version, for example `1.4.1` to `1.4.2`.
   Keep `major.minor.patch`. `npm version 1.4.2 --no-git-tag-version` updates
   `package.json` and `package-lock.json`. Also update the app crate version in
   `src-tauri/Cargo.toml` and `src-tauri/Cargo.lock`. Tauri reads the package version. The Store
   version is that value plus `.0`, so the package after `1.4.1.0` is `1.4.2.0`,
   not `1.4.1.1`.
2. Commit and push to `main`, then push a matching tag such as `v1.4.2`. Do not
   move an existing tag.
3. After the tagged Windows MSIX build succeeds, download
   `Contrast21_windows_x64.msix` from the artifact or GitHub Release.
4. In Partner Center, upload that MSIX. Confirm the version is the
   `package.json` version plus `.0`, declare capabilities including
   `runFullTrust`, and submit.

Do not upload the `.cer`, installer script, or artifact ZIP. Rebuilding or
renaming the same version does not replace a published package.

**Linux desktop**

With Rust and the Tauri system dependencies installed:

```bash
npm run tauri -- build --config src-tauri/tauri.linux.conf.json
```

The Debian package is written under `src-tauri/target/release/bundle/deb/`.

