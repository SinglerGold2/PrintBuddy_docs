# PrintBuddy - Projektstatus

[🇬🇧 English Version](PROJECT_STATE.md)

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

Stand: 24.09.2026 (lokal)
Versionsstand: `0.10.6`

## Ziel

Ein stabiles, professionelles Stream-Deck-Plugin für 3D-Drucker-Monitoring und -Steuerung mit strikt instanz-lokaler Einstellungsisolation.

## Status

### Erledigt

- Release-Version auf `0.10.6` über Manifest, Paketmetadaten, Build-Metadaten und Dokumentation synchronisiert.
- Die Einstellungen für Status, Status FX und MultiExtruder sind in lokalisierte Tabs gegliedert.
- Status-FX-Gauges unterstützen eine separate Sichtbarkeit je Datentyp, einstellbare Temperaturbereiche sowie Farben für normale Werte und Werte über 100 %.
- Ring-, Bogen- und Kreis-Gauges halten Beschriftungen und Werte gut lesbar.
- Der leer erscheinende Tab „Anzeigeoptionen“ wurde behoben; er war fälschlich in einem anderen Tab-Bereich enthalten.
- Preset-Theme-Laden in der Runtime korrigiert: Alle Theme-Definitionen werden in `src/core/themes/theme-registry.ts` jetzt statisch importiert, wodurch die Rollup-inkompatible `import.meta.glob`-Abhängigkeit entfällt.
- Verifiziert, dass Nicht-Benutzer-Presets über Classic-, Neon-Glow- und Cyber-Varianten hinweg wieder zuverlässig ihre eigenen Paletten/Text-Defaults anwenden.
- Moonraker-Adressen ohne expliziten Port verwenden jetzt den Fallback `7125`; fehlende Ports und ungültige Antworten werden lokalisiert dargestellt.
- Dynamisches Text-Auto-Fit und begrenzter Zeilenumbruch stehen für kompakte Stream-Deck-Tastentexte zur Verfügung.
- Lokalisierte Druckerstatus-Meldungen werden durch einen einheitlichen Oberkanten-Vertrag zwischen Textlayout und SVG-Ausgabe zentriert.
- PrintBuddy Status nutzt einen zentralen Renderer für Hintergründe, Meldungen und Telemetrie und behält die bestehende Theme-/Style-Geometrie bei.
- Klingon-Locale und zugehöriges Flaggen-Asset vollständig entfernt.
- Die 12 aktiven Locales sind zentralisiert; PI-Kataloge werden aus den TypeScript-Runtime-Locales generiert.
- Arabisch schaltet Property Inspectoren auf RTL; alle anderen Locales stellen LTR wieder her.
- Der i18n-Audit prüft Katalogparität, generierte Ausgabe, Flaggen, Script-Reihenfolge und entfernte Locale-Referenzen.
- Generische Core-Dateinamen wurden durch eindeutige Modulnamen ersetzt.
- Exakte Entwicklungsumgebung und getestete Geräte in der Dokumentation ergänzt: Windows 11, Visual Studio Code v1.137.0, Stream Deck Target v7.5.1, Stream Deck MK.2, Stream Deck XL, Stream Deck Plus (v1).
- Historische Release-Zeitstempel in den Patchnotes für verfügbare getaggte Versionen anhand von Git-Tag-Metadaten korrigiert.
- Status-Badges in der Dokumentation auf das native GitHub-Workflow-Badge-Format umgestellt.
- Querverweis auf die vollständige Versionshistorie weiterhin gültig: [PATCHNOTES.de.md](PATCHNOTES.de.md).
- Repository-Dokumentation über alle Markdown-Dateien hinweg aktualisiert und standardisiert.
- EN/DE-Dokumentationsarchitektur beibehalten und erweitert.
- Referenzbasierter Array-Vergleich in der Multitool-Settings-Synchronisierung durch wertbasierten Vergleich ersetzt, um wiederholte Rewrites zu verhindern.
- Flackernde IP-Eingabe im Multitool-Property-Inspector behoben (verursacht durch Settings-Echo-Loops).
- Zuverlässiges Extruder-Auswahlverhalten in Lite/Pro wiederhergestellt (Auswahl/Abwahl, Reihenfolge, Labels, Vier-Tool-Limit).
- Lite/Pro-Multitool-Regressions-Tests ergänzt und ohne Netzwerkzugriff validiert.
- Synchronisierten Lite/Pro-Build- und Release-Ablauf (`build`, `build:lite`, `build:pro`) mit expliziter Editions-Paritätsprüfung verbindlich gemacht.
- Gebündelte Theme-JSON-Dateien normalisiert (einheitliche Struktur/Formatierung, garantiertes `logo`-Objekt) und JSON-kompatible Theme-Metadaten auf Englisch standardisiert.

### In Arbeit

- Die physische Stream-Deck-Prüfung läuft aktuell für stabile Multitool-IP-Eingabe sowie Lite/Pro-Extruderinteraktionen.

### Blockiert

- Keine technischen Blocker.

## Validierung

- `npm run build`: für Release `0.10.6` erfolgreich.
- `npm run i18n:audit`: mit 13 aktiven Locales und 166 Referenzschlüsseln erfolgreich.
- `npx tsc --noEmit`: erfolgreich.
- `node scripts/test-status-webcam.mjs`: erfolgreich.
- `node scripts/test-multitool.mjs`: erfolgreich.
- Das generierte Plugin-Bundle enthält den korrigierten SVG-Vertrag `dominant-baseline="text-before-edge"`.
- Das generierte Plugin-Bundle enthält eindeutige Preset-Tokens (z. B. Prusa/Klipper/Synthwave) und bestätigt damit die statische Theme-Registrierung im Output.
- Isolierter Property-Inspector-Smoke-Test: für alle 12 Locales, arabisches RTL und LTR-Wiederherstellung erfolgreich.

## Mandatory Pre-Release Pipeline

Whenever a version bump occurs (minor, major, or documentation patch), ALL related files must be automatically and synchronously updated in one step:

- `package.json`, `package-lock.json`, `manifest.json`
- `README.md` & `README.de.md` (Version badge/text)
- `PROJECT_DESCRIPTION.md` & `PROJECT_DESCRIPTION.de.md` (Version status)
- `PROJECT_STATE.md` & `PROJECT_STATE.de.md` (Version status & validation logs)
- `PATCHNOTES.md` & `PATCHNOTES.de.md` (Changelog entry with short reason)

Verbindliche Ausführungsreihenfolge:

1. Alle versionsführenden Dateien aus obiger Liste synchron aktualisieren.
2. `node scripts/i18n-audit.mjs` ausführen.
3. `npm run build` ausführen.
4. Validierungsergebnisse in `PROJECT_STATE.md` / `PROJECT_STATE.de.md` dokumentieren.
5. Release committen und inkl. Tags pushen.

## Vollstaendige Release-Historie

- Fuer die vollstaendige Versionshistorie siehe [PATCHNOTES.de.md](PATCHNOTES.de.md).


