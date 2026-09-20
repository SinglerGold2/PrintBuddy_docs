# PrintBuddy - Project State

[🇩🇪 Deutsche Version](PROJECT_STATE.de.md)

<p align="center">
  <img src="com.ulli.printbuddy.sdPlugin/imgs/printerbuddy_logo.jpg" alt="PrintBuddy Logo" width="220" />
</p>

<h1 align="center">PrintBuddy</h1>

<p align="center">
  <a href="https://github.com/SinglerGold2/PrintBuddy/actions/workflows/build.yml">
    <img src="https://github.com/SinglerGold2/PrintBuddy/actions/workflows/build.yml/badge.svg" alt="Build Status" />
  </a>
  <img src="https://img.shields.io/badge/version-v0.9.1-blue" alt="Version" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Windows-supported-0078D6?logo=windows&logoColor=white" alt="Windows" />
  <img src="https://img.shields.io/badge/macOS-supported-000000?logo=apple&logoColor=white" alt="macOS" />
</p>

Status date: 20.09.2026 (local)
Version status: `0.9.1`

## Goal

Deliver a stable, professional Stream Deck plugin for 3D printer monitoring and control with strict per-instance settings isolation.

## State

### Done

- Release version synchronized to `0.9.1` across manifest, package metadata, build metadata and documentation.
- Status, Status FX and MultiExtruder settings are organized into localized tabs.
- Status FX gauges support separate visibility per data type, configurable temperature ranges and colours for normal and over-100% values.
- Ring, arc and segmented gauge layouts keep their labels and values readable.
- Fixed the Gauge Options tab appearing empty because it was incorrectly contained in another tab panel.
- Fixed preset-theme runtime loading: all theme definitions are now statically imported in `src/core/themes/theme-registry.ts`, removing the Rollup-incompatible `import.meta.glob` dependency.
- Verified that non-user presets now reliably apply their own palettes/text defaults across Classic, Neon Glow and Cyber variants.
- Moonraker addresses without an explicit port now fall back to `7125`; missing-port and invalid-response states are localized.
- Dynamic text auto-fit and bounded wrapping are available for compact Stream Deck button text.
- Localized printer-status messages are centered through a consistent top-edge contract between text layout and SVG serialization.
- PrintBuddy Status uses a central renderer for backgrounds, messages and telemetry while preserving existing theme/style geometry.
- Klingon locale support and its flag asset were removed completely.
- The 12 active locales are centralized and PI catalogs are generated from runtime TypeScript locale sources.
- Arabic switches Property Inspectors to RTL; all other locales restore LTR.
- The i18n audit validates catalog parity, generated output, flags, script order and removed-locale references.
- Generic core filenames were replaced by descriptive module names.
- Integrated exact development environment specs and tested devices into documentation: Windows 11, Visual Studio Code v1.137.0, Stream Deck Target v7.5.1, Stream Deck MK.2, Stream Deck XL, Stream Deck Plus (v1).
- Corrected historical release timestamps in patch notes via Git tag metadata for available tagged versions.
- Migrated status badges across documentation to the native GitHub workflow badge format.
- Confirmed full release history cross reference remains valid: [PATCHNOTES.md](PATCHNOTES.md).
- Repository documentation update and standardization across all Markdown files.
- EN/DE documentation architecture maintained and expanded.
- Replaced reference-based array comparison in Multitool settings synchronization with value-based comparison to prevent repeated rewrites.
- Fixed Multitool Property Inspector IP input flickering caused by settings echo loops.
- Restored reliable extruder selection handling in Lite/Pro (select/deselect, order, labels, four-tool cap).
- Added Lite/Pro Multitool regression tests and confirmed they run without network access.

### In Progress

- Physical Stream Deck verification is in progress for Multitool IP entry stability and Lite/Pro extruder interaction behavior.

### Blocked

- No technical blockers.

## Validation

- `npm run build`: passed for release `0.9.1`.
- `npm run i18n:audit`: passed with 12 active locales and 149 reference keys.
- `npx tsc --noEmit`: passed.
- `node scripts/test-status-webcam.mjs`: passed.
- `node scripts/test-multitool.mjs`: passed.
- Generated plugin bundle contains the corrected `dominant-baseline="text-before-edge"` SVG contract.
- Generated plugin bundle contains distinct preset tokens (e.g. Prusa/Klipper/Synthwave), confirming static theme registration in output.
- Isolated Property Inspector smoke test: passed for all 12 locales, Arabic RTL and LTR restoration.

## Mandatory Pre-Release Pipeline

Whenever a version bump occurs (minor, major, or documentation patch), ALL related files must be automatically and synchronously updated in one step:

- `package.json`, `package-lock.json`, `manifest.json`
- `README.md` & `README.de.md` (Version badge/text)
- `PROJECT_DESCRIPTION.md` & `PROJECT_DESCRIPTION.de.md` (Version status)
- `PROJECT_STATE.md` & `PROJECT_STATE.de.md` (Version status & validation logs)
- `PATCHNOTES.md` & `PATCHNOTES.de.md` (Changelog entry with short reason)

Required execution order:

1. Update all version-bearing files listed above.
2. Run `node scripts/i18n-audit.mjs`.
3. Run `npm run build`.
4. Record validation output in `PROJECT_STATE.md` / `PROJECT_STATE.de.md`.
5. Commit and push release branch with tags.

## Full Release History

- For the complete version history, see [PATCHNOTES.md](PATCHNOTES.md).

