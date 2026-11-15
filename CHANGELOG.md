# Changelog

## 1.5.1 - 2026-11-14

### Improved

- Harmony options line up on the left, with the checkmark in the label.
- Click a Harmony contrast swatch to apply that color.
- New screenshots and a clearer store description.

### Windows release

- Microsoft Store MSIX package version 1.5.1.0.

## 1.5.0 - 2026-11-13

### Added

- Ctrl+Shift+F and Ctrl+Shift+B jump to the foreground and background color tuners.

### Improved

- Color fields now say “Color” instead of “Color...”
- Color count, contrast, and Regenerate sit together under the Harmony wheel.
- Harmony swatches sit beside the wheel on larger screens, and above contrast palettes on smaller ones.
- Hex codes appear under Harmony and contrast swatches.
- Minimum contrast labels no longer end with a colon.
- Harmony controls sit beside the wheel, with brightness below.
- Harmony palettes stay to the right when there’s room, with lock and contrast on one line.

### Fixed

- Harmony markers spread around the selected hue.
- The swap colors button shows on small screens.
- Hue and saturation sliders work when the color is white or black.
- Lightness no longer shifts saturation.
- The color panel no longer scrolls sideways.
- Harmony’s Regenerate button makes new random palettes.

### Windows release

- Microsoft Store MSIX package version 1.5.0.0.

## 1.4.5 - 2026-11-07

### Added

- Microsoft Store titles and descriptions in all ten languages, collected in LISTINGS.md.
- Two new screenshots.

### Improved

- The language chooser shows English names beside native names.

### Windows release

- Microsoft Store MSIX package version 1.4.5.0.

## 1.4.4 - 2026-11-07

### Fixed

- Windows release builds accept both Windows and Unix line endings in the lockfile check.

### Windows release

- Microsoft Store MSIX package version 1.4.4.0.

## 1.4.3 - 2026-11-07

### Added

- Microsoft Store titles and descriptions in all ten languages.

### Fixed

- Light, dark, and system appearance are remembered.
- Contrast21 naming is consistent, including the page title.

### Windows release

- Microsoft Store MSIX package version 1.4.3.0.

## 1.4.2 - 2026-11-07

### Added

- English, Spanish, French, German, Brazilian Portuguese, Simplified Chinese, Japanese, Korean, Hindi, and Arabic.
- Choose a language in the tools rail, or follow the system language.
- Right-to-left layout for Arabic.

### Fixed

- System default follows browser language changes.
- Color slider gradients work in right-to-left layout.
- Language names are clearer for screen readers.

### Changed

- Translations live in one JSON file per language.
- Tests cover every required plural form.

### Windows release

- Microsoft Store MSIX package version 1.4.2.0.

## 1.4.1 - 2026-11-06

### Improved

- The Windows eyedropper hex label is smoother and easier to read.
- A thin grid on the lens helps you pick a specific pixel.

## 1.4.0 - 2026-11-05

### Fixed

- The Windows eyedropper no longer swaps red and blue.

### Changed

- Click to pick a color. Right-click to cancel.

### Windows release

- Microsoft Store MSIX package version 1.4.0.0.

## 1.3.9 - 2026-11-05

### Improved

- The Windows eyedropper is more stable, with the same following lens, color label, and crosshair.
- Unused Pick panel pieces, icons, and fonts are gone. Saved palettes are unchanged.

### Windows release

- Partner Center needs package versions that end in `.0`. Bump the patch number for a new package.
- Microsoft Store MSIX package version 1.3.9.0.

## 1.3.8 - 2026-11-04

### Improved

- Import My Colors as `color name: #hex`. Names can include spaces.
- In the Grid panel, Ctrl+Shift plus an arrow moves one cell.
- Shorter help text in Harmony, eyedropper, and contrast suggestions.
- The Windows eyedropper follows the pointer with a circular lens.
- Arrow keys move the pointer while the Windows picker is open.
- The window can be narrower than before.
- Copy a Harmony contrast set as CSS custom properties.
- The color refinement panel keeps its background and swatches without an extra scrollbar.

### Windows release

- Microsoft Store MSIX package version 1.3.8.0.

## 1.3.7 - 2026-11-01

### Improved

- Switch between light, dark, and system appearance.
- Faster keyboard shortcuts and navigation.
- A larger color wheel for refining colors.
- Apply Harmony colors to your foreground or background.

### Windows release

- Microsoft Store MSIX package version 1.3.7.0.

## 1.3.0 - 2026-10-30

### Improved

- The color panel stays centered on small screens and lines up with the selected color on desktop.
- Contrast ratios no longer shift the header.
- Choose AA or AAA for generated palettes. AAA is the default.
- Clearer foreground and background labels in the contrast grid.

### Windows release

- Microsoft Store MSIX package version 1.3.0.0.

## 1.2.0 - 2026-10-29

### Windows release

- The Microsoft Store MSIX is the default Windows package. Build it with `npm run package:msix`.
- Package identity matches Contrast21 - Accessibility Color Checker.

## 1.1 - 2026-10-28

### Improved

- Generate Harmony palettes from your background without changing the selected colors.
- Hold Shift for slower wheel movement. Brightness reaches pure black.
- Palettes of 5, 6, or 7 colors, with grouped Regenerate and Import buttons.
- See every imported swatch in My Colors, with editable names and copy-all buttons.
- Consistent Harmony and My Colors button styling.
- Pick is selected when the app opens. Clearer tool labels on small screens.
- Scrollbars sit against panel edges. Help and branding stay put.
- A blue icon on the tools rail and a compact wordmark in panel footers.

### Windows release

- Windows x64 app and MSI installer.
- Requires Microsoft Edge WebView2. Keep `WebView2Loader.dll` beside the standalone executable.
- Builds are unsigned.
