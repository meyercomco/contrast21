# Changelog

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
- Package identity matches the reserved Store app, Contrast 21 - Accessibility Color Checker.

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


