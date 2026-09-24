# PrintBuddy

## Display text and positions (v0.10.7)

Printer states and display messages are localized across 13 languages. Labels,
values, tool text, messages and Control dial text have independent X/Y offsets.
In **Pro → User Theme**, expand the text-position controls to edit them. Fixed
presets and Lite use the positions defined by their theme; zero offsets preserve
the existing layout. Pro's **Save as…** stores offsets in `text.positions`.

Regression coverage: `npm run test:text`. Visual checks on Stream Deck hardware,
especially dial alignment and clipping, remain outstanding.

## Provider integration (v0.10.6)

Pro and Lite offer **Klipper / Moonraker** (default for existing profiles), **local PrusaLink v1** and **Bambu LAN (local)** in every included Property Inspector. Provider selection is not an edition difference. For Bambu LAN, enter the local printer address, serial number and LAN access code; real-printer validation remains outstanding. For PrusaLink, enter the printer's local address and either an API key (where supported by firmware) or its PrusaLink username/password for HTTP Digest authentication. An API key takes precedence. Do not use Prusa Connect cloud credentials.

- Prusa status: nozzle/bed temperature, progress, state, filename, remaining time, Z position, speed/flow and print-fan RPM when supplied by firmware. Polling is at least one second per action, with five-second request timeouts and automatic recovery.
- Prusa controls: **Pause, Resume, Cancel**. Cancel retains hold-to-confirm. **Emergency Stop is not mapped to job cancellation.** Lights, Speed Dial and free-form G-code are unavailable.
- MultiExtruder displays the reported current nozzle in slot T0. Individual XL tool mapping is not implemented or verified; other slots show unknown values. This is an integration limit, not a claim of technical impossibility.
- Prusa webcams require an explicit, independently accessible snapshot URL. Printer credentials are never forwarded to webcam hosts.
- Credentials are stored in Stream Deck action settings (not an encrypted vault). Avoid exporting profiles with secrets; use HTTPS where supported or a trusted local network. Redirects are rejected; TLS verification remains enabled.
- Legacy PrusaLink `/api/printer`-only firmware and Prusa Connect cloud are not implemented or verified. Provider hints are translated in all 13 languages. Leave the API key empty when using username/password; find credentials on the printer under Settings → Network → PrusaLink.
- Job details are optional: missing details, network failures and detail timeouts preserve the current base status. Authentication failures and explicit cancellation are not hidden. Only matching job IDs are merged; old filenames and measurements are not retained between polls. Finite numeric strings are accepted; only progress is clamped to 0–100% (not speed/flow). Missing progress remains unknown.

Technical reference: [Gantrybar attribution and MIT notice](com.ulli.printbuddy.sdPlugin/THIRD-PARTY-NOTICES.md), pinned to a specific revision and included in both Pro and Lite distributions. Additional Prusa controls remain unimplemented/unverified and are not enabled by this reference.

Validation: `npm run test:providers`, existing control/status/webcam/multitool/theme tests, TypeScript and Pro/Lite builds. Physical-printer and Stream Deck UI smoke tests remain necessary before release.

[🇩🇪 Deutsche Version](README.de.md)

## Template logos (v0.10.0)

Anycubic, Bambu Lab, Creality, Elegoo, Elgato, FlashForge, Fluidd, Klipper,
OctoPrint, Prusa, Snapmaker and Voron now use matching tintable
SVG background logos. Themes without an assignment retain the existing action
appearance. **User Theme → Template Logo** offers logo, color, opacity and size;
in Pro, **Save as…** stores the assignment in a custom theme. Developers configure
fixed templates in their JSON files. Control operation symbols remain in front;
webcam snapshots are unchanged.

The [SVG/theme guide](com.ulli.printbuddy.sdPlugin/themes/README.md) covers
`currentColor`, `viewBox`, sizing and registering additional logos.
Source sites: allsvgicons.com and svgrepo.com. Per-asset license clearance remains
outstanding; see [third-party notices](com.ulli.printbuddy.sdPlugin/THIRD-PARTY-NOTICES.md).
Regression test: `npm run test:logos`.

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

Stream Deck plugin for monitoring and controlling 3D printers (focused on Klipper/Moonraker).

**Current Version:** `0.10.7`

## Changelog (v0.10.6)

- Enforced synchronized Lite/Pro delivery: shared `build`/`build:lite`/`build:pro` workflow plus parity checks for versions, manifests, shared UI/providers and approved edition differences.
- Normalized all bundled theme JSON files with consistent formatting and a guaranteed `logo` object (`id: "none"` fallback where no logo is assigned).
- Added JSON-compatible theme metadata (`_header`, `_comment`) and `_ipNotice` on branded/logo themes; standardized metadata text to English.
- Hardened theme parity validation to compare parsed JSON instead of raw text, so formatting-only updates do not trigger false mismatches.
- Validation passed locally with `npm run build`, `npm run test:logos` and `npm run test:editions`; real-device Bambu LAN verification remains the final hardware step.

## Changelog (v0.10.0)

- Added shared provider integration for local PrusaLink v1 (API key or Digest auth) across all Property Inspectors in Pro and Lite, while keeping Moonraker as default.
- Added tintable template-logo pipeline and expanded selectable logo IDs to Anycubic, Bambu Lab, Creality, Elegoo, Elgato, FlashForge, Fluidd, Klipper, OctoPrint, Prusa, Snapmaker and Voron.
- Added logo source/prepare/test workflow (`assets/logo-sources` → `scripts/prepare-theme-logos.mjs` → `imgs/logos`) plus updated theme and legal documentation.

## Changelog (v0.9.2)

- Removed risky/non-working theme file actions from the Property Inspector; only safe theme-file flow remains.
- Theme file actions now expose only **Save as…** (`themes:save`) and **Reload** (`themes:reload`).
- Removed backend handling for the obsolete **open folder** command.
- Expanded user-theme documentation for save/reload workflow, naming rules, JSON schema structure and validation expectations.

## Changelog (v0.8.0)

- Reorganized the settings for Status, Status FX and MultiExtruder into clear tabs.
- Expanded Status FX gauges with display controls, temperature ranges, gauge colours and a separate colour for speed or flow above 100%.
- Gauge visibility can now be set separately for each selected data type.
- Improved gauge layouts so labels and values remain readable in the different gauge shapes.
- Fixed the empty Gauge Options tab and improved saving and restoring of Property Inspector settings.
- Added all new labels to the 12 supported languages.

## Changelog (v0.7.21)

- Theme-provided `valueFontSize` and `labelFontSize` values are now editable after theme selection in Property Inspectors.
- Manual font-size overrides now persist correctly for non-user themes across save/reopen/update cycles.
- Theme changes still apply recommended default text sizes once during selection.
- Hid the Button Style selector from Property Inspectors while preserving internal compatibility and Classic default behavior.

## Changelog (v0.7.7)

- Fixed preset-theme application across Classic, Neon Glow and Cyber buttons: non-user presets now reliably apply their own palette and text defaults.
- Replaced fragile `import.meta.glob` theme discovery with explicit static theme imports in `src/core/themes/theme-registry.ts` so Rollup always bundles all presets.
- Preserved `USER_THEME` behavior: custom Property Inspector values stay editable and continue to override only for the user theme.
- Validated with `npx tsc --noEmit`, `npm run build` and `npm run i18n:audit`; generated bundle contains distinct palette tokens for presets like Prusa/Klipper/Synthwave.

## Overview

- Multiple actions for status, FX/gauges, multi-tool monitoring, webcam and printer control
- Theme system with centralized presets
- Theme-specific text defaults (status/message)
- Runtime + Property Inspector localization across 13 active locales
- Generated Property Inspector catalogs sourced from the canonical TypeScript runtime locales
- Per-key `en_gb` fallback and automatic RTL/LTR direction handling for Arabic
- Automatic build metadata and DIN 5008 timestamp in all Property Inspector footers
- Rehydration of selected language flag icons in Property Inspectors

## Changelog (v0.7.5)

- Added Moonraker port `7125` fallback and localized diagnostics for missing ports and invalid responses.
- Added dynamic text auto-fit and intentional line wrapping for compact 144x144 Stream Deck keys.
- Centered localized missing-IP, offline and connection-error messages by aligning SVG baselines with the text layout engine.
- Centralized PrintBuddy Status rendering while preserving the established theme and button-style composition.

## Changelog (v0.6.7)

- Removed the Klingon locale and its flag asset completely.
- Centralized the 12 active locales and generated Property Inspector catalogs from the runtime locale sources.
- Added Arabic RTL support, strict locale/catalog auditing and complete translation-key parity.
- Replaced generic `index.ts` and `settings.ts` modules with descriptive, function-based filenames.

## Changelog (v0.6.4)

- Property Inspector i18n flag path and locale normalization fixes for all supported languages.
- Dynamic language dropdown registration and immediate DOM re-translation on locale switch.
- Comprehensive JS/TS JSDoc expansion and Markdown visual header integration.

## Changelog (v0.6.2)

- Repository documentation update and standardization across all Markdown files.

## Changelog (v0.6.1)

- Standardized dual-language documentation architecture across repository markdown files (EN/DE).
- Cleaned up public documentation and removed internal build validation log fragments.
- Synchronized project state and release versioning to `0.6.1`.

## Changelog (v0.6.0)

- **i18n Lazy Loading & Performance Boost:** Dynamic language loading significantly reduces plugin startup load.
- **ISO-Underscore Standardization:** Unified locale and flag naming scheme (`de_de`, `en_gb`, `fr_fr`, ...).
- **Build Metadata & PI Footer:** Automatic version and DIN 5008 timestamp (`YYYYMMDD.HHmm`) in all Property Inspectors.

## Development

#### Requirements
- Node.js
- npm

#### Development Environment
- OS: Windows 11
- Editor: Visual Studio Code v1.137.0
- Stream Deck Target: v7.5.1
- Tested Devices: Stream Deck MK.2, Stream Deck XL, Stream Deck Plus (v1)

#### Commands
- `npm run i18n:generate`
- `npm run i18n:audit`
- `npm run build`: builds the source plugin, Lite and Pro together, then verifies edition parity.
- `npm run build:lite` / `npm run build:pro`: compatibility aliases for the same shared build; no one-sided updates.
- `npm run test:editions`: checks existing builds for matching versions/timestamps, current shared UI files, all three providers and approved manifest/theme differences.
- `npm run watch`: updates all three build targets; restarts Lite and Pro after a successful parity check.

**Required edition policy:** Lite and Pro must always share the same source, version and common feature level. Only previously agreed differences are allowed (existing Status FX, theme/customization and extruder limits); new differences require prior agreement. Bambu LAN is available in both editions. Stream Deck must point to the respective `dist/lite` and `dist/pro` plugin directories; a Git push alone does not update an installation.

## Third-Party Assets

- Icon attribution: `com.ulli.printbuddy.sdPlugin/licences/ICON_ATTRIBUTION.md`

## Full Release History

- For the complete version history, see [PATCHNOTES.md](PATCHNOTES.md).

