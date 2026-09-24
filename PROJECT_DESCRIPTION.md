# PrintBuddy - Project Description

[🇩🇪 Deutsche Version](PROJECT_DESCRIPTION.de.md)

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

Last updated: 24.09.2026 (local)
Version status: `0.10.6`

## Goal

PrintBuddy is a Stream Deck plugin for monitoring and controlling 3D printers (currently focused on Klipper/Moonraker).

## Current feature scope

- Instance-local settings per key
- Consistent theme/rendering logic
- Robust defaults and fallback handling
- Moonraker endpoint normalization with default port `7125` and localized connection diagnostics
- Central 144x144 status-button renderer with dynamic auto-fit, wrapping and bounded text layout
- Runtime + Property Inspector localization across 12 canonical locales
- Generated PI locale catalogs with per-key English fallback and Arabic RTL support
- Tabbed Property Inspectors for Status, Status FX and MultiExtruder
- Configurable Status FX gauges with per-data visibility, ranges, colours and multiple gauge shapes
- Multitool settings synchronization hardened with value-based comparison for `selectedExtruders` to prevent PI save loops and IP input flicker
- Stable Lite/Pro extruder selection behavior with preserved order, labels and four-tool cap
- Descriptive core module names for localization, action settings, themes and style rendering
- Standardized English JSDoc SDK headers across core and PI shared modules
- Shared Lite/Pro build & parity workflow with enforced version/manifest/UI/provider synchronization
- Normalized bundled theme JSON metadata/structure with semantic parity validation support

## Actions

- PrintBuddy Status
- PrintBuddy Status FX
- PrintBuddy MultiExtruder
- PrintBuddy WebCam
- PrintBuddy Control

## Notes

- Build metadata and DIN 5008 timestamps are rendered in PI footers.
- Theme and text defaults are synchronized across core/runtime/PI.
- Theme preset resolution is now statically registered for Rollup compatibility, ensuring all non-user presets are always bundled and applied.
- Runtime locale sources are the single source of truth for generated Property Inspector translations.
- Message rendering uses top-edge SVG baselines to match the text layout engine and keep localized status messages centered.
- Gauge labels and values adapt to the selected ring, arc or segmented layout.

## Full Release History

- For the complete version history, see [PATCHNOTES.md](PATCHNOTES.md).


