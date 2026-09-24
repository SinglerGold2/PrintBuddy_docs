# i18n-Refactoring-Log

[🇬🇧 English Version](i18n-refactoring-log.md)

Versionsbezug: `0.9.2`

## Umfang

- ISO-Underscore-Namensschema für Locales und Flaggen zwischen Runtime und Property Inspector vereinheitlicht.
- Runtime-i18n auf dynamisches Lazy Loading der Locale-Kataloge umgestellt.
- Locale-Normalisierung für Aliase, Kurzcodes und Mischformate gehärtet.
- Klingon-Unterstützung und zugehöriges Flaggen-Asset entfernt; 12 aktive Locales verbleiben.
- `src/core/i18n/active-locales.ts` als kanonische Liste aktiver Locales eingeführt.
- Property-Inspector-Kataloge werden während des Builds aus den TypeScript-Runtime-Locale-Modulen generiert.
- Druckerverbindungsdiagnosen (`missingIp`, `offline`, `portMissing`, `invalidResponse` und verwandte Zustände) sind in allen 12 aktiven Locales vollständig und enthalten beabsichtigte Zeilenumbrüche für begrenzte Tastenlayouts.

## Zentrale Ergebnisse

- Dynamisches Nachladen von Locales per asynchroner Modulauflösung.
- In-Memory-Cache für bereits geladene Locale-Kataloge.
- Einheitliche Locale-Keys in PI-Sprachauswahl und Flaggen-Rendering.
- Schlüsselweiser `en_gb`-Fallback ohne vollständige englische Katalogkopien.
- Arabische Property Inspectoren verwenden RTL; alle anderen Locales stellen LTR wieder her.
- Neue Property-Inspector-Tabs und Status-FX-Gauge-Einstellungen sind in allen 12 aktiven Locales verfügbar.
- `npm run i18n:audit` prüft Schlüsselparität, Flaggen, generierte Bundle-Parität, PI-Script-Reihenfolge und entfernte Locale-Referenzen.
- Lokalisierte Runtime-Meldungen verwenden das gemeinsame dynamische Textlayout und den SVG-Oberkanten-Baseline-Vertrag, damit Übersetzungslängen Meldungsblöcke nicht vertikal verschieben.

## Module

- Runtime-Lokalisierungs-Gateway: `src/core/i18n/localization.ts`
- Kanonische Locale-Liste: `src/core/i18n/active-locales.ts`
- PI-Kataloggenerator: `scripts/generate-pi-i18n.mjs`
- Generierter Browser-Katalog: `com.ulli.printbuddy.sdPlugin/ui/shared/i18n-locales.js`
- Gemeinsamer Tastenrenderer: `src/core/render/ButtonRenderer.ts`
- SVG-Textserialisierung: `src/core/render/text-render.ts`

