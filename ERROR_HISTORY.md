# Error History

[🇩🇪 Deutsche Version](ERROR_HISTORY.de.md)

<p align="center">
  <img src="com.ulli.printbuddy.sdPlugin/imgs/printerbuddy_logo.jpg" alt="PrintBuddy Logo" width="220" />
</p>

<h1 align="center">PrintBuddy</h1>

<p align="center">
  <a href="https://github.com/SinglerGold2/PrintBuddy/actions/workflows/build.yml">
    <img src="https://github.com/SinglerGold2/PrintBuddy/actions/workflows/build.yml/badge.svg" alt="Build Status" />
  </a>
  <img src="https://img.shields.io/badge/version-v0.10.6-blue" alt="Version" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Windows-supported-0078D6?logo=windows&logoColor=white" alt="Windows" />
  <img src="https://img.shields.io/badge/macOS-supported-000000?logo=apple&logoColor=white" alt="macOS" />
</p>

Status date: 24.09.2026
Version: `0.10.6`

## [FIXED] Multitool IP input flickered and extruder selection could reset

- **Summary:** Multitool settings normalization compared `selectedExtruders` arrays by reference. Equivalent arrays were treated as changed, triggering repeated save/write-back loops and causing Property Inspector IP field flicker and unstable extruder selection behavior.
- **Affected area:** `src/actions/multitool-monitor.ts`, `com.ulli.printbuddy.sdPlugin/ui/multitool-monitor.html`
- **Fixed in:** `0.9.2`
- **Resolution:** Switched to value-based settings comparison for normalized Multitool fields, preserved dynamic controls and active edits during refresh, and added regression tests for Lite/Pro selection behavior without network access.
- **Status:** Fixed; physical Stream Deck spot verification is in progress.

## [FIXED] Gauge Options tab appeared empty

- **Summary:** Gauge settings were hidden together with the Theme tab, making the selected Gauge Options tab appear empty.
- **Affected area:** PrintBuddy Status FX settings.
- **Fixed in:** `0.8.0`
- **Resolution:** Restored the intended tab separation so gauge controls remain inside their own panel.
- **Status:** Fixed; final in-app verification remains open.

## [FIXED] Non-user theme presets could render with fallback PrintBuddy palette

- **Summary:** Theme registry discovery depended on `import.meta.glob` which is unavailable in this Rollup runtime path, so non-user presets were not reliably bundled and runtime fell back to PrintBuddy palette values.
- **Affected area:** `src/core/themes/theme-registry.ts`, preset palette/text resolution for Classic, Neon Glow and Cyber button variants.
- **Fixed in:** `0.7.21`
- **Resolution:** Replaced glob-based discovery with explicit static imports of all theme definitions and kept immutable preset resolution semantics.
- **Status:** Fixed

## [FIXED] Localized printer-status messages were vertically shifted or clipped

- **Summary:** SVG output treated text layout coordinates as midpoint baselines although the layout engine supplied top edges, causing multi-line missing-IP and connection-error messages to render too low or clip.
- **Affected area:** `src/core/render/text-render.ts`, `src/core/render/ButtonRenderer.ts` and PrintBuddy Status message rendering.
- **Fixed in:** `0.7.5`
- **Resolution:** SVG text now uses `dominant-baseline="text-before-edge"`; PrintBuddy Status routes background, message and telemetry rendering through the central `ButtonRenderer`.
- **Status:** Fixed; final on-device locale spot-check remains a release validation task.

## [FIXED] Moonraker addresses without explicit ports produced unclear failures

- **Summary:** A configured host without a port could lead to connection errors without distinguishing missing-port and invalid-response conditions.
- **Affected area:** Moonraker endpoint normalization, action settings and localized status diagnostics.
- **Fixed in:** `0.7.5`
- **Resolution:** Added port `7125` fallback and complete localized `portMissing`/`invalidResponse` coverage across all 12 active locales.
- **Status:** Fixed

## [FIXED] Property Inspector locale catalogs diverged from runtime sources

- **Summary:** Property Inspectors maintained a separate translation implementation and could drift from runtime locale catalogs; an obsolete Klingon locale also remained exposed.
- **Affected area:** Runtime/PI localization, language selectors, fallback behavior and Arabic directionality.
- **Fixed in:** `0.6.7`
- **Resolution:** PI catalogs are generated from the 12 canonical runtime locales, obsolete locale assets were removed, per-key fallback was added and RTL/LTR switching is audited.
- **Status:** Fixed

## [FIXED] printer-status-fx payload/save syntax issue

- **Summary:** Invalid brace/block structure in the Property Inspector affected payload return flow and persistence reliability.
- **Affected area:** `buildPayload()` / `save()` in `com.ulli.printbuddy.sdPlugin/ui/printer-status-fx.html`
- **First reported:** `0.5.11`
- **Fixed in:** `0.5.4`
- **Status:** Fixed

## [FIXED] Theme preset inconsistency (core vs PI)

- **Summary:** Not all themes were consistently available across core, PI and i18n layers.
- **Affected area:** Theme selection and text fallback behavior in runtime + PI.
- **First reported:** `0.0.3.1`
- **Fixed in:** `0.0.3.2`
- **Status:** Fixed

## [FIXED] Missing per-theme text defaults

- **Summary:** Actions did not consistently apply theme-specific text defaults.
- **Affected area:** Status/message text fallback behavior during theme changes.
- **First reported:** `0.0.3.1`
- **Fixed in:** `0.0.3.2`
- **Status:** Fixed

## Full Release History

- For the complete version history, see [PATCHNOTES.md](PATCHNOTES.md).


