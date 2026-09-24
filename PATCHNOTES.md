# Patch Notes

## Version 0.10.7 - 24.09.2026

### Changes

- Localized printer display states and messages across 13 language catalogs.
- Added independent theme-backed X/Y offsets for labels, values, tool text, messages and Control dial text. Zero offsets preserve the existing layout.
- Text positions are editable only in Pro with User Theme selected; fixed presets and Lite inherit theme-defined positions. Pro theme files persist them under `text.positions`.
- Preserved Control Lite preset selection, mapped Multitool offsets by tool ID and separated shifted dial text into independent overlay layers.
- Added regressions for text positioning, localization, theme persistence, settings stability and edition restrictions.
- Includes the Control preset refactor, logo offsets and the Creality preset for Lite. Physical Stream Deck checks for alignment and clipping remain outstanding.

## Version 0.10.6 - 24.09.2026

### Changes

- Normalized all bundled theme JSON files to a consistent structure and formatting, including a guaranteed `logo` object (`id: "none"` default where no logo is assigned).
- Added JSON-compatible metadata fields (`_header`, `_comment`) across themes and `_ipNotice` for branded/logo themes, with all metadata text standardized to English.
- Updated edition parity checks to compare theme JSON semantically (parsed JSON), preventing false mismatches from formatting/metadata-only edits.
- Kept Lite/Pro synchronized through the shared build/parity flow and validated locally with `npm run build`, `npm run test:logos`, and `npm run test:editions`.

## Version 0.10.5 - 23.09.2026

### Changes

- Made source-plugin, Lite and Pro builds a shared workflow (including `build:lite`/`build:pro`); added parity checks for version/timestamp, shared UI, providers and existing edition boundaries. Bambu LAN is not Pro-exclusive. Watch updates and restarts both editions.
- Added shared **Bambu LAN provider** support through `BambuLanClient`, wired via `provider: bambu` in the provider factory and action/provider settings flow.
- Added/validated Bambu command scope mapping for `pause`, `resume`, `cancel` (`cancel` maps to `stop`) and aligned action-side connectivity/offline error rendering.
- Added webcam URL mode resolution (`jpeg`, `rtsp`, `rtsps`) and telemetry normalization behavior for Bambu, including chamber temperature fallback handling.
- Extended provider lifecycle/recovery test coverage across MQTT connect/subscribe/pushall/ping/reconnect paths.
- Local validation passed with `npm run build` and `node scripts/test-providers.mjs`; live Bambu hardware verification remains the final release-gate step.

## Version 0.10.0 - 23.09.2026

### Changes

- Translated Prusa hints into all 13 languages; clarified API-key precedence and leaving the key empty for Digest. Control limitations remain Control-only.
- Added tintable template background logos for twelve brands, including dropdown, color, opacity, size, theme-file persistence and the existing action fallback without a logo.
- Added SVG preparation, developer documentation and rendering/persistence regression checks. Recorded allsvgicons.com/svgrepo.com provenance; per-asset license clearance is still required before publication.

- Local PrusaLink v1 with API-key/Digest authentication, status polling and pause/resume/cancel.
- Shared provider selection and credential persistence in all five Property Inspectors, Pro and Lite.
- Moonraker remains the default; command endpoints and G-code compatibility fallback are preserved.
- Unsupported Prusa operations are blocked, including emergency stop; explicit webcam snapshot URL required.
- Added mocked provider regressions. Hardware validation is outstanding; see README for scope and security notes.
- Hardened optional Prusa job details, numeric-string parsing and progress bounds; added regressions for job changes, missing data, authentication failures and detail cancellation. Added pinned Gantrybar attribution/MIT notice to both distributions.

[🇩🇪 Deutsche Version](PATCHNOTES.de.md)

<p align="center">
  <img src="com.ulli.printbuddy.sdPlugin/imgs/printerbuddy_logo.jpg" alt="PrintBuddy Logo" width="220" />
</p>

<h1 align="center">PrintBuddy</h1>

<p align="center">
  <a href="https://github.com/SinglerGold2/PrintBuddy/actions/workflows/build.yml">
    <img src="https://github.com/SinglerGold2/PrintBuddy/actions/workflows/build.yml/badge.svg" alt="Build Status" />
  </a>
  <img src="https://img.shields.io/badge/version-v0.10.7-blue" alt="Version" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Windows-supported-0078D6?logo=windows&logoColor=white" alt="Windows" />
  <img src="https://img.shields.io/badge/macOS-supported-000000?logo=apple&logoColor=white" alt="macOS" />
</p>

## Version 0.9.2 - 23.09.2026

### Changes

- Removed risky/non-working theme file actions from Property Inspectors and kept only the safe theme file workflow.
- Property Inspector theme actions now support only `themes:save` (Save as…) and `themes:reload` (Reload).
- Removed obsolete backend handling for `themes:openFolder`.
- Added/expanded user-theme documentation with naming rules, save/reload flow, JSON structure and validation constraints.
- Preserved Pro build output user-theme folder during rebuild cleanup to avoid deleting user theme files/docs.

## Version 0.8.0 - 17.09.2026

### Changes

- Reorganized the Status, Status FX and MultiExtruder settings into clear tabs for easier navigation.
- Expanded Status FX gauge options with per-data visibility, temperature ranges, configurable colours and an over-100% colour for speed and flow.
- Improved the layout and scaling of values and labels across ring, arc and segmented gauges.
- Fixed the Gauge Options tab appearing empty and made Property Inspector settings more reliable when saving, reopening or switching themes.
- Added complete translations for the new tabs and gauge settings across all 12 supported languages.

## Version 0.7.21 - 17.09.2026

### Changes

- Allowed Property Inspector overrides for theme-provided `valueFontSize` and `labelFontSize` values.
- Ensured manual font-size changes persist even when a non-user preset theme is active.
- Preserved one-time theme default application during theme switching.
- Hid the Property Inspector Button Style selector while preserving existing internal bindings and Classic fallback behavior.
- Revalidated runtime normalization, Property Inspector persistence and Rollup build output.

## Version 0.7.7 - 16.09.2026

### Changes

- Fixed preset theme loading in runtime by replacing non-Rollup-compatible `import.meta.glob` discovery with explicit static imports in `src/core/themes/theme-registry.ts`.
- Ensured non-user theme presets now apply their complete own palette and text defaults across Classic, Neon Glow and Cyber button variants.
- Preserved user theme behavior where custom persisted Property Inspector values remain editable and theme-local.
- Revalidated TypeScript, build and i18n audit pipelines and confirmed generated bundle includes unique preset palette/text tokens (e.g. Prusa, Klipper, Synthwave).

## Version 0.7.5 - 16.09.2026

### Changes

- Added a default Moonraker port fallback to `7125` when an address is configured without an explicit port.
- Added localized `port missing` and `invalid response` messages to all 12 active runtime and Property Inspector catalogs, including intentional line breaks for 144x144 keys.
- Introduced a dynamic text layout engine with auto-fit, wrapping, maximum-line and bounded-height support.
- Corrected the SVG text serialization contract from midpoint baselines to top-edge baselines, preventing vertically shifted or clipped localized messages.
- Added the central `ButtonRenderer` for PrintBuddy Status backgrounds, message buttons and telemetry text while preserving the proven 72x72 composition at 144x144 scale.
- Kept missing-IP and offline informational states on a neutral background and ensured localized strings are used throughout the affected action paths.
- Validated build, TypeScript compilation, generated bundle baseline and i18n parity across 12 active locales and 140 reference keys.

## Version 0.7.0 - 15.09.2026

### Changes

- Corrected theme resolution so PrintBuddy remains the absolute base, presets replace the complete palette and only the user theme applies individual Property Inspector overrides.
- Added canonical `baseColor2` background stops across Classic, Neon Glow and Cyber Tech. The original `baseColor_Cyber` value `#0f1a2a` and `baseColor_ring` default `#39ff14` remain readable for settings migration only.
- Applied linear and radial gradient directions dynamically, including reversed stops for `edge-to-center`.
- Removed the original hard Cyber Tech background fallback `#000000` and placed its matrix artwork above the resolved theme gradient as an overlay.
- Added stronger full-height Cyber Tech brackets with stroke width `2.5`. The original matrix overlay opacity `0.96` and Neon Glow border width `1.25` remain unchanged.
- Preserved the original direction fallbacks `top-right` and `center-to-edge` while separating direction persistence per button style.
- Removed the legacy `src/core/theme` compatibility wrappers and migrated consumers to `src/core/themes`.

## Version 0.6.7 - 15.09.2026

### Changes

- Removed the Klingon locale, aliases, translation options and flag asset.
- Established `src/core/i18n/active-locales.ts` as the canonical list of 12 supported locales.
- Added build-time generation of `ui/shared/i18n-locales.js` from the TypeScript runtime catalogs.
- Reworked Property Inspector localization with per-key `en_gb` fallback and Arabic RTL/LTR switching.
- Expanded the i18n audit to validate locale/key parity, flag assets, generated bundle parity, script order and removed-locale references.
- Completed missing gradient-direction translations in all active catalogs.
- Renamed generic core modules to `action-settings.ts`, `i18n/localization.ts`, `themes/theme-registry.ts` and `graphics/styles/button-style-renderer.ts`.

## Version 0.6.6 - 15.09.2026

### Changes

- Fixed i18n locale switching for non-English and non-German locale files by providing full static fallback loaders in the former `src/core/i18n/index.ts` module.

## Version 0.6.5 - 15.09.2026

### Changes

- Documented exact development environment specs and tested hardware devices (Stream Deck MK.2, XL, Plus v1), corrected historical release timestamps via git tag metadata, and migrated to native GitHub workflow status badges.

## Version 0.6.4 - 15.09.2026

### Changes

- Complete patchnote history backfill across all previous releases.
- Updated all documentation build badges to the GitHub Actions workflow URL with explicit main branch targeting.
- Synchronized release metadata and version references to 0.6.4.

## Version 0.6.3 - 15.09.2026

### Changes

- Fixed Property Inspector locale flag asset resolution for all 13 supported languages.
- Enforced strict lowercase underscore locale normalization to prevent PI 404 errors.
- Removed hardcoded language registration paths and populated locale dropdowns dynamically from loaded translations.
- Ensured immediate re-translation of all data-i18n bound PI elements on language change.
- Synchronized PI footer version display with build and manifest release version v0.6.3.
- Added and expanded English JSDoc coverage across JS and TS functions, methods, and classes.
- Integrated a standardized visual HTML header into all release and project markdown documents.

## Version 0.6.2 - 14.09.2026

### Changes

- Repository documentation update and standardization across all markdown files.

## Version 0.6.1 - 14.09.2026

### Changes

- Standardized dual-language documentation architecture across all repository markdown files.
- Cleaned up public documentation from internal build validation logs.
- Synchronized project state and versioning to 0.6.1.

## Version 0.6.0 - 14.09.2026

### Changes

- Introduced dynamic runtime i18n lazy loading with per-locale async imports and cache.
- Standardized locale and flag naming to ISO underscore format.
- Added automatic build metadata and DIN 5008 timestamp footer support for all Property Inspectors.

## Version 0.5.17 - 14.09.2026

### Changes

- Standardized locale and flag naming to ISO underscore conventions across runtime and PI.

## Version 0.5.16 - 14.09.2026

### Changes

- Implemented dynamic locale registry and PI flag icon handling for multilingual Property Inspectors.

## Version 0.5.15 - 13.09.2026

### Changes

- Fixed neon radial gradient direction mapping and style-specific gradient consistency.

## Version 0.5.11 - 13.09.2026

### Changes

- Added patchnotes tracking and synchronized release metadata to 0.5.11.

## Version 0.5.10 - 14.09.2026

### Changes

- Synchronized markdown documentation set and release version metadata.

## Version 0.5.7 - 14.09.2026

### Changes

- Centralized i18n locale to flag mapping and dynamic PI language dropdown handling for all supported languages.

## Version 0.5.6 - 14.09.2026

### Changes

- Refactored network and IP persistence responsibilities into protected core module boundaries.
- Synchronized documentation and release metadata.

## Version 0.5.4 - 14.09.2026

### Changes

- Standardized English JSDoc headers and release documentation metadata.

## Version 0.5.3 - 14.09.2026

### Changes

- Updated markdown documentation and release synchronization texts.

## Version 0.5.2 - 14.09.2026

### Changes

- Updated project documentation set and synchronized release metadata.

## Version 0.5.1 - 14.09.2026

### Changes

- Established early release baseline for modular runtime and documentation flow.

## Version 0.1.1 - 14.09.2026

### Changes

- Performed first maintenance release after initial public versioning baseline.

## Version 0.1.0 - 14.09.2026

### Changes

- Introduced first formal semantic release bump to 0.1.0.

