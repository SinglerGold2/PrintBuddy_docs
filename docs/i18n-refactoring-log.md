# i18n Refactoring Log

[🇩🇪 Deutsche Version](i18n-refactoring-log.de.md)

Version reference: `0.9.2`

## Scope

- ISO-underscore locale and flag naming standardized across runtime and Property Inspector.
- Runtime i18n switched to dynamic lazy loading for locale catalogs.
- Locale normalization hardened for aliases, short codes and mixed formats.
- Klingon support and its flag asset removed; 12 active locales remain.
- `src/core/i18n/active-locales.ts` established as the canonical active-locale list.
- Property Inspector catalogs generated from TypeScript runtime locale modules during builds.
- Printer connection diagnostics (`missingIp`, `offline`, `portMissing`, `invalidResponse` and related states) are complete in all 12 active locales, with intentional line breaks for constrained button layouts.

## Key outcomes

- Dynamic locale loading via asynchronous module resolution.
- In-memory caching for loaded locale catalogs.
- Unified locale key usage in PI language selectors and flag rendering.
- Per-key `en_gb` fallback without cloning entire English catalogs.
- Arabic Property Inspectors use RTL and all other locales restore LTR.
- New Property Inspector tabs and Status FX gauge settings are available in all 12 active locales.
- `npm run i18n:audit` verifies key parity, flags, generated bundle parity, PI script order and removed-locale references.
- Localized runtime messages use the shared dynamic text layout and top-edge SVG baseline contract so translation length does not shift message blocks vertically.

## Modules

- Runtime localization gateway: `src/core/i18n/localization.ts`
- Canonical locale list: `src/core/i18n/active-locales.ts`
- PI catalog generator: `scripts/generate-pi-i18n.mjs`
- Generated browser catalog: `com.ulli.printbuddy.sdPlugin/ui/shared/i18n-locales.js`
- Shared button renderer: `src/core/render/ButtonRenderer.ts`
- SVG text serializer: `src/core/render/text-render.ts`

