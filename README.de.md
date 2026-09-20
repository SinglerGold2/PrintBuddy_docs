# PrintBuddy

[🇬🇧 English Version](README.md)

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

Stream-Deck-Plugin zur Überwachung und Steuerung von 3D-Druckern (Fokus: Klipper/Moonraker).

**Aktuelle Version:** `0.9.1`

## Changelog (v0.9.1)

- Das Flackern des IP-Feldes im Multitool-Property-Inspector wurde behoben, indem wiederholte Einstellungs-Überschreibungen durch referenzbasierte Array-Vergleiche verhindert wurden.
- Das Extruder-Auswahlverhalten in Lite und Pro wurde korrigiert; Reihenfolge, Labels und das Vier-Tool-Limit bleiben mit wertbasierter Normalisierung stabil.
- Regressions-Tests für die Persistenz der Multitool-Auswahl ergänzt, ohne Moonraker-/HTTP-Netzwerkpfade zu verändern.
- Dynamische Tool-Steuerelemente und aktive Eingaben im Property Inspector bleiben während der Einstellungssynchronisierung erhalten.

## Changelog (v0.8.0)

- Die Einstellungen für Status, Status FX und MultiExtruder wurden in übersichtliche Tabs gegliedert.
- Status-FX-Gauges bieten jetzt Anzeigeoptionen, Temperaturbereiche, Gauge-Farben und eine eigene Farbe für Geschwindigkeit oder Fluss über 100 %.
- Die Gauge-Anzeige lässt sich für jeden ausgewählten Datentyp separat festlegen.
- Die Anordnung der Gauges wurde verbessert, damit Beschriftungen und Werte in allen Gauge-Formen gut lesbar bleiben.
- Der leere Tab „Anzeigeoptionen“ wurde behoben und das Speichern sowie Wiederherstellen der Einstellungen verbessert.
- Alle neuen Beschriftungen wurden in die 12 unterstützten Sprachen aufgenommen.

## Changelog (v0.7.21)

- Theme-vorgegebene `valueFontSize`- und `labelFontSize`-Werte können nach der Theme-Auswahl jetzt im Property Inspector bearbeitet werden.
- Manuelle Schriftgrößen-Overrides bleiben nun auch bei Nicht-Benutzer-Themes über Speichern, Neuladen und Updates hinweg erhalten.
- Theme-Wechsel setzen weiterhin einmalig empfohlene Standard-Schriftgrößen.
- Die Auswahl „Button Style“ wurde im Property Inspector ausgeblendet, während interne Kompatibilität und das Classic-Standardverhalten erhalten bleiben.

## Changelog (v0.7.7)

- Preset-Theme-Anwendung für Classic-, Neon-Glow- und Cyber-Buttons korrigiert: Nicht-Benutzer-Presets wenden jetzt zuverlässig ihre eigene Palette und Text-Defaults an.
- Fragile Theme-Erkennung per `import.meta.glob` in `src/core/themes/theme-registry.ts` durch explizite statische Theme-Imports ersetzt, damit Rollup alle Presets sicher bündelt.
- Verhalten von `USER_THEME` beibehalten: benutzerdefinierte Property-Inspector-Werte bleiben editierbar und übersteuern weiterhin nur beim Benutzer-Theme.
- Validiert mit `npx tsc --noEmit`, `npm run build` und `npm run i18n:audit`; das generierte Bundle enthält eindeutige Preset-Farbtokens (z. B. Prusa/Klipper/Synthwave).

## Überblick

- Mehrere Actions für Status, FX/Gauges, Multitool-Monitoring, Webcam und Druckersteuerung
- Theme-System mit zentralen Presets
- Theme-spezifische Textdefaults (Status/Message)
- Lokalisierung für Runtime und Property Inspector in 12 aktiven Locales
- Generierte Property-Inspector-Kataloge aus den kanonischen TypeScript-Runtime-Locales
- Schlüsselweiser `en_gb`-Fallback und automatische RTL/LTR-Ausrichtung für Arabisch
- Automatische Build-Metadaten und DIN-5008-Zeitstempel in allen Property-Inspector-Footern
- Rehydrierung der ausgewählten Sprach-Flaggen in den Property Inspectoren

## Changelog (v0.7.5)

- Moonraker-Port-Fallback `7125` und lokalisierte Diagnosen für fehlende Ports und ungültige Antworten ergänzt.
- Dynamische Textanpassung und beabsichtigte Zeilenumbrüche für kompakte 144x144-Stream-Deck-Tasten ergänzt.
- Lokalisierte Meldungen für fehlende IP, Offline- und Verbindungsfehler durch abgestimmte SVG-Baselines zentriert.
- Rendering der PrintBuddy-Status-Taste zentralisiert und die bestehende Theme-/Button-Style-Komposition beibehalten.

## Changelog (v0.6.7)

- Klingon-Locale und zugehöriges Flaggen-Asset vollständig entfernt.
- Die 12 aktiven Locales zentralisiert und PI-Kataloge aus den Runtime-Quellen generiert.
- Arabische RTL-Unterstützung, strikten Locale-/Katalog-Audit und vollständige Schlüsselparität ergänzt.
- Generische `index.ts`- und `settings.ts`-Module durch eindeutige, funktionsbezogene Dateinamen ersetzt.

## Changelog (v0.6.4)

- Property-Inspector-i18n-Flaggenpfade und Locale-Normalisierung für alle unterstützten Sprachen korrigiert.
- Dynamische Sprachregistrierung im Dropdown und sofortige DOM-Neuübersetzung bei Sprachwechsel.
- Umfassende JS/TS-JSDoc-Erweiterung und Integration des visuellen Markdown-Headers.

## Changelog (v0.6.2)

- Update der Repository-Dokumentation und Standardisierung über alle Markdown-Dateien hinweg.

## Changelog (v0.6.1)

- Zweisprachige Dokumentationsarchitektur im Repository vereinheitlicht (EN/DE).
- Öffentliche Dokumentation von internen Build-/Validierungsprotokollen bereinigt.
- Projektstatus und Versionierung auf `0.6.1` synchronisiert.

## Changelog (v0.6.0)

- **i18n Lazy Loading & Performance Boost:** Dynamisches Nachladen von Sprachen reduziert die Startlast des Plugins deutlich.
- **ISO-Underscore-Standardisierung:** Einheitliches Locale-/Flag-Schema (`de_de`, `en_gb`, `fr_fr`, ...).
- **Build-Metadaten & PI-Footer:** Automatische Anzeige von Version und DIN-5008-Zeitstempel (`YYYYMMDD.HHmm`) in allen Property Inspectoren.

## Entwicklung

#### Voraussetzungen
- Node.js
- npm

#### Entwicklungsumgebung
- Betriebssystem: Windows 11
- Editor: Visual Studio Code v1.137.0
- Stream Deck Basis: v7.5.1
- Getestete Geräte: Stream Deck MK.2, Stream Deck XL, Stream Deck Plus (v1)

#### Befehle
- `npm run i18n:generate`
- `npm run i18n:audit`
- `npm run build`

## Drittanbieter-Assets

- Icon-Attribution: `com.ulli.printbuddy.sdPlugin/licences/ICON_ATTRIBUTION.de.md`

## Vollstaendige Release-Historie

- Fuer die vollstaendige Versionshistorie siehe [PATCHNOTES.de.md](PATCHNOTES.de.md).
