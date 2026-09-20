# PrintBuddy - Projektbeschreibung

[🇬🇧 English Version](PROJECT_DESCRIPTION.md)

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

Letzte Aktualisierung: 20.09.2026 (lokal)
Versionsstand: `0.9.1`

## Ziel

PrintBuddy ist ein Stream-Deck-Plugin zur Überwachung und Steuerung von 3D-Druckern (aktuell mit Fokus auf Klipper/Moonraker).

## Aktueller Funktionsumfang

- Instanz-lokale Einstellungen pro Taste
- Konsistente Theme-/Rendering-Logik
- Robuste Defaults und Fallback-Mechanismen
- Moonraker-Endpunktnormalisierung mit Standard-Port `7125` und lokalisierten Verbindungsdiagnosen
- Zentraler 144x144-Status-Tastenrenderer mit dynamischem Auto-Fit, Umbruch und begrenztem Textlayout
- Lokalisierung in Runtime und Property Inspector über 12 kanonische Locales
- Generierte PI-Locale-Kataloge mit schlüsselweisem Englisch-Fallback und arabischer RTL-Unterstützung
- Property Inspectoren mit Tabs für Status, Status FX und MultiExtruder
- Konfigurierbare Status-FX-Gauges mit datentypabhängiger Sichtbarkeit, Wertebereichen, Farben und mehreren Gauge-Formen
- Gehärtete Multitool-Settings-Synchronisierung mit wertbasiertem Vergleich von `selectedExtruders`, um PI-Save-Loops und IP-Eingabe-Flackern zu verhindern
- Stabiles Extruder-Auswahlverhalten in Lite/Pro mit erhaltener Reihenfolge, Labels und Vier-Tool-Limit
- Eindeutige Core-Modulnamen für Lokalisierung, Action-Einstellungen, Themes und Style-Rendering
- Standardisierte englische JSDoc-SDK-Header in Core- und PI-Shared-Modulen

## Actions

- PrintBuddy Status
- PrintBuddy Status FX
- PrintBuddy MultiExtruder
- PrintBuddy WebCam
- PrintBuddy Control

## Hinweise

- Build-Metadaten und DIN-5008-Zeitstempel werden im PI-Footer dargestellt.
- Theme- und Textdefaults sind über Core/Runtime/PI synchronisiert.
- Die Theme-Preset-Auflösung ist jetzt statisch für Rollup-Kompatibilität registriert, sodass alle Nicht-Benutzer-Presets stets gebündelt und angewendet werden.
- Die Runtime-Locale-Quellen sind die einzige Quelle für die generierten Property-Inspector-Übersetzungen.
- Die Meldungsausgabe verwendet SVG-Oberkanten-Baselines passend zur Text-Layout-Engine, damit lokalisierte Statusmeldungen zentriert bleiben.
- Gauge-Beschriftungen und Werte passen sich an das gewählte Ring-, Bogen- oder Kreis-Layout an.

## Vollstaendige Release-Historie

- Fuer die vollstaendige Versionshistorie siehe [PATCHNOTES.de.md](PATCHNOTES.de.md).

