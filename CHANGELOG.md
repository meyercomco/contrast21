# Changelog

## 1.5.0 - 2026-11-13

### Added

- Keyboard shortcuts Ctrl+Shift+F and Ctrl+Shift+B now focus the foreground and background tuner toggle buttons respectively, allowing you to press Enter to open the color refinement panel.

### Improved

- Simplify the color input placeholder text from "Color..." to "Color" in English and Spanish translations.
- Place color count, minimum contrast, and Regenerate together beneath the Harmony color wheel; remove redundant section headings.
- Show the Harmony palette beside the wheel on medium and larger panels with wrapping swatches, and above the contrast palettes on smaller panels with matching scaled columns.
- Display hex codes below Harmony swatches and on a separate line beneath bottom-aligned sample text inside foreground and background contrast swatches.
- Remove trailing colons from minimum contrast labels in all ten languages.
- Place Harmony controls beside the color wheel while keeping the brightness slider below it; use equal-width harmony choices, with two columns when space permits.
- Keep the Harmony palette to the right when space permits and below the wheel otherwise; display each swatch label on one line with the lock first and any contrast badge after the ratio.

### Fixed

- Spread Harmony color-wheel markers around the selected hue instead of stacking extra swatches under the pointer.
- Show the swap colors button on small screens, where it was previously hidden.
- Let hue and saturation sliders respond in the color refinement panel when white or black is selected, instead of staying stuck at 0.
- Keep saturation steady while moving the lightness slider instead of shifting as the color is rounded to hex.
- Remove the horizontal scrollbar from the color refinement panel by keeping slider thumbs inside their tracks.
- Fix the Regenerate button in Harmony panel to produce truly random color variations instead of repeating in a fixed 4-step cycle.

### Windows release

- Microsoft Store MSIX package version 1.5.0.0.

## 1.4.5 - 2026-11-07

### Added

- Collect translated Microsoft Store titles and descriptions for all ten languages in LISTINGS.md.
- Add two application screenshots.

### Improved

- Show English language names beside native names in the language chooser, preserving native capitalization and isolating text direction for Arabic.

### Windows release

- Microsoft Store MSIX package version 1.4.5.0.

## 1.4.4 - 2026-11-07

### Fixed

- Accept Windows CRLF and Unix LF line endings in the Rust lockfile version check so Windows release builds can pass the test step.

### Windows release

- Microsoft Store MSIX package version 1.4.4.0.

## 1.4.3 - 2026-11-07

### Added

- Translated Microsoft Store descriptions and application titles in all ten language dictionaries.

### Fixed

- Remember light, dark, or system appearance across application launches and initialize colors using the saved preference.
- Use Contrast21 consistently in application branding and update the page title to match the selected language.

### Windows release

- Microsoft Store MSIX package version 1.4.3.0.

## 1.4.2 - 2026-11-07

### Added

- Support English, Spanish, French, German, Brazilian Portuguese, Simplified Chinese, Japanese, Korean, Hindi, and Arabic throughout the interface.
- Choose a language from the tools rail or follow the system language, with the selection saved on your device.
- Support right-to-left layout for Arabic and translated control labels, help text, and plural messages.

### Fixed

- Follow browser language changes while System default is selected, and use the browser's primary language when its preference list is empty.
- Align color slider gradients with right-to-left slider behavior.
- Identify language names for screen readers and avoid duplicate initialization listeners.

### Changed

- Use i18next for locale matching and text direction, and Intl.DisplayNames for native language names. Adding a language requires one JSON dictionary and one registration entry.
- Check every required plural form in translation tests.

### Windows release

- Microsoft Store MSIX package version 1.4.2.0.

## 1.4.1 - 2026-11-06

### Improved

- Draw the Windows eyedropper's hex label with anti-aliased Consolas text instead of the blocky built-in bitmap font.
- Add a thin grid over the Windows eyedropper lens, aligned to the magnified source pixels, to make it easier to pick a specific pixel.

## 1.4.0 - 2026-11-05

### Fixed

- Correct the Windows eyedropper’s floating swatch and hex label, which had red and blue reversed. Use the same COLORREF conversion as the selected color.

### Changed

- Remove unreliable arrow-key pointer movement and its help text. Use click to select a color and right-click to cancel.

### Windows release

- Microsoft Store MSIX package version 1.4.0.0.

## 1.3.9 - 2026-11-05

### Improved

- Use Windows' built-in lens scaling instead of the custom pixel-copy callback implicated in picker crashes. Keep the cursor-following lens, color label, crosshair, and keyboard controls.
- Read the live color through a GDI-owned bitmap and sample the final selection after hiding the lens.
- Preserve the working overlay bitmap if a DPI resize allocation fails, and check bitmap selection errors.
- Remove the unused pixel-grid command, superseded Pick panel, inactive session editing methods, unused icons, and unused fonts. Existing saved palette data is left intact.
- Add Windows development checks and regression coverage for color ordering and overlay drawing bounds.

### Windows release

- Reject MSIX package versions whose revision is not 0. Partner Center accepts only `major.minor.patch.0`; increase the patch number to publish another package.
- Microsoft Store MSIX package version 1.3.9.0.

## 1.3.8 - 2026-11-04

### Improved

- Import My Colors as `color name: #hex`. Names can include spaces, and pasted Harmony values drop a leading `--` and trailing `;`.
- In the Grid panel, Ctrl+Shift with an arrow moves one cell in that direction and previews it, even when focus starts outside the grid. Hold Ctrl to see those arrow hints around the center cell.
- Shorten panel help text so the Harmony, eyedropper, and contrast suggestions are easier to read.
- Windows eyedropper draws a circular lens that follows the pointer, instead of a fixed preview inside the app.
- Arrow keys and Shift+arrows move the pointer while the Windows picker is active, including when the app is not in front.
- The desktop window can be resized narrower than the previous 920px floor.
- Copy a full Harmony contrast set from the With my foreground or With my background title as CSS custom properties, starting with foreground and background, then color1, color2, and so on.
- Restore the color refinement panel background and keep its web-color swatches visible without an extra scrollbar.

### Windows release

- Microsoft Store MSIX package version 1.3.8.0.

## 1.3.7 - 2026-11-01

### Improved

- Switch between light, dark, and system appearance.
- Work faster with keyboard shortcuts and improved keyboard navigation through color swatches and controls.
- Refine colors with a larger color wheel.
- Apply Harmony colors to your selected foreground or background.

### Windows release

- Synchronize the app version and local MSIX packaging defaults for Microsoft Store package version 1.3.7.0.

## 1.3.0 - 2026-10-30

### Improved

- Refine colors in a panel that stays centered on smaller screens and aligns with the selected color card on desktop.
- Read contrast ratios without the header shifting as values change.
- Choose AA or AAA contrast targets for generated palettes, with AAA selected by default.
- Identify foreground and background colors more easily with clearer contrast grid labels.

### Windows release

- Microsoft Store MSIX package version 1.3.0.0.

## 1.2.0 - 2026-10-29

### Windows release

- The Microsoft Store MSIX is the default Windows package. Build it with `npm run package:msix`.
- Package identity matches the reserved Store app, Contrast21 - Accessibility Color Checker.

## 1.1 - 2026-10-28

### Improved

- Generate Harmony palettes from your current background color without changing your selected foreground or background.
- Fine-tune colors with slower wheel movement while holding Shift and a brightness slider that reaches pure black. A single active handle makes overlapping palette colors easier to select.
- Choose palettes of 5, 6, or 7 colors with clearer selection controls and conveniently grouped Regenerate and Import to My Colors buttons.
- View every imported swatch in My Colors, with collections that fit the panel, editable names, and buttons to copy entire collections.
- Harmony and My Colors action buttons now share consistent colors, hover feedback, and keyboard focus styling.
- Pick is selected when the app opens. Bold uppercase tool labels and inline icons make the horizontal menu easier to scan on smaller screens.
- Content scrollbars now sit against panel edges, while help and footer branding remain outside the scrolling content.
- Refreshed branding adds a blue icon to the desktop tools rail and a compact wordmark to panel footers.

### Windows release

- Includes a Windows x64 application and MSI installer built from Ubuntu.
- Requires Microsoft Edge WebView2. Keep `WebView2Loader.dll` beside the standalone executable.
- Builds are unsigned; installation, launch, upgrade, and uninstall still require verification on Windows.


