# Fehlerhistorie

[🇬🇧 English Version](ERROR_HISTORY.md)

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

Stand: 20.09.2026
Version: `0.9.1`

## [BEHOBEN] Multitool-IP-Eingabe flackerte und Extruder-Auswahl konnte zurückspringen

- **Kurzbeschreibung:** Die Multitool-Settings-Normalisierung verglich `selectedExtruders`-Arrays per Referenz. Inhaltlich gleiche Arrays wurden als Änderung gewertet, was wiederholte Save/Write-back-Schleifen auslöste und zu flackernder IP-Eingabe sowie instabilem Extruder-Auswahlverhalten führte.
- **Betroffener Bereich:** `src/actions/multitool-monitor.ts`, `com.ulli.printbuddy.sdPlugin/ui/multitool-monitor.html`
- **Behoben in:** `0.9.1`
- **Lösung:** Auf wertbasierten Vergleich normalisierter Multitool-Felder umgestellt, dynamische Controls und aktive Eingaben beim Refresh erhalten und Lite/Pro-Regressions-Tests ohne Netzwerkzugriff ergänzt.
- **Status:** Behoben; physische Stream-Deck-Stichprobe läuft.

## [BEHOBEN] Tab „Anzeigeoptionen“ erschien leer

- **Kurzbeschreibung:** Die Gauge-Einstellungen wurden zusammen mit dem Theme-Tab ausgeblendet, sodass der ausgewählte Tab „Anzeigeoptionen“ leer erschien.
- **Betroffener Bereich:** Einstellungen von PrintBuddy Status FX.
- **Behoben in:** `0.8.0`
- **Lösung:** Die vorgesehene Tab-Trennung wurde wiederhergestellt, sodass die Gauge-Einstellungen in ihrem eigenen Bereich bleiben.
- **Status:** Behoben; die finale Prüfung in Stream Deck steht noch aus.

## [BEHOBEN] Nicht-Benutzer-Theme-Presets konnten mit PrintBuddy-Fallbackpalette gerendert werden

- **Kurzbeschreibung:** Die Theme-Registry-Erkennung hing von `import.meta.glob` ab, was in diesem Rollup-Runtime-Pfad nicht verfügbar ist. Dadurch wurden Nicht-Benutzer-Presets nicht zuverlässig gebündelt und die Runtime fiel auf PrintBuddy-Palettenwerte zurück.
- **Betroffener Bereich:** `src/core/themes/theme-registry.ts`, Preset-Palette-/Textauflösung für Classic-, Neon-Glow- und Cyber-Button-Varianten.
- **Behoben in:** `0.7.21`
- **Lösung:** Glob-basierte Erkennung durch explizite statische Imports aller Theme-Definitionen ersetzt und unveränderliche Preset-Auflösungssemantik beibehalten.
- **Status:** Behoben

## [BEHOBEN] Lokalisierte Druckerstatus-Meldungen waren vertikal verschoben oder abgeschnitten

- **Kurzbeschreibung:** Die SVG-Ausgabe interpretierte Textlayout-Koordinaten als Mittelpunkt-Baselines, obwohl die Layout-Engine Oberkanten lieferte. Dadurch wurden mehrzeilige Meldungen für fehlende IP und Verbindungsfehler zu tief oder abgeschnitten dargestellt.
- **Betroffener Bereich:** `src/core/render/text-render.ts`, `src/core/render/ButtonRenderer.ts` und Meldungsrendering von PrintBuddy Status.
- **Behoben in:** `0.7.5`
- **Lösung:** SVG-Text verwendet jetzt `dominant-baseline="text-before-edge"`; PrintBuddy Status führt Hintergrund-, Meldungs- und Telemetrie-Rendering über den zentralen `ButtonRenderer` aus.
- **Status:** Behoben; die finale Locale-Stichprobe auf dem Gerät bleibt eine Release-Validierungsaufgabe.

## [BEHOBEN] Moonraker-Adressen ohne expliziten Port führten zu unklaren Fehlern

- **Kurzbeschreibung:** Ein konfigurierter Host ohne Port konnte Verbindungsfehler auslösen, ohne fehlenden Port und ungültige Antwort eindeutig zu unterscheiden.
- **Betroffener Bereich:** Moonraker-Endpunktnormalisierung, Action-Einstellungen und lokalisierte Statusdiagnosen.
- **Behoben in:** `0.7.5`
- **Lösung:** Port-Fallback `7125` und vollständige lokalisierte Abdeckung für `portMissing`/`invalidResponse` in allen 12 aktiven Locales ergänzt.
- **Status:** Behoben

## [BEHOBEN] Property-Inspector-Locale-Kataloge wichen von Runtime-Quellen ab

- **Kurzbeschreibung:** Property Inspectoren pflegten eine separate Übersetzungsimplementierung, die von den Runtime-Katalogen abweichen konnte; zusätzlich blieb ein veraltetes Klingon-Locale sichtbar.
- **Betroffener Bereich:** Runtime-/PI-Lokalisierung, Sprachauswahl, Fallback-Verhalten und arabische Schreibrichtung.
- **Behoben in:** `0.6.7`
- **Lösung:** PI-Kataloge werden aus den 12 kanonischen Runtime-Locales generiert, veraltete Locale-Assets wurden entfernt, schlüsselweiser Fallback ergänzt und RTL/LTR-Umschaltung wird auditiert.
- **Status:** Behoben

## [BEHOBEN] printer-status-fx Payload-/Save-Syntaxproblem

- **Kurzbeschreibung:** Eine ungültige Block-/Klammerstruktur im Property Inspector störte den Payload-Rückgabefluss und die Persistenz.
- **Betroffener Bereich:** `buildPayload()` / `save()` in `com.ulli.printbuddy.sdPlugin/ui/printer-status-fx.html`
- **Erstmals gemeldet:** `0.5.11`
- **Behoben in:** `0.5.4`
- **Status:** Behoben

## [BEHOBEN] Theme-Preset-Inkonsistenz (Core vs. PI)

- **Kurzbeschreibung:** Themes waren nicht in allen Ebenen (Core, PI, i18n) konsistent verfügbar.
- **Betroffener Bereich:** Theme-Auswahl und Text-Fallback-Verhalten in Runtime + PI.
- **Erstmals gemeldet:** `0.0.3.1`
- **Behoben in:** `0.0.3.2`
- **Status:** Behoben

## [BEHOBEN] Fehlende per-Theme Textdefaults

- **Kurzbeschreibung:** Actions nutzten theme-spezifische Textdefaults nicht durchgängig.
- **Betroffener Bereich:** Status-/Message-Text-Fallbacks bei Theme-Wechsel.
- **Erstmals gemeldet:** `0.0.3.1`
- **Behoben in:** `0.0.3.2`
- **Status:** Behoben

## Vollstaendige Release-Historie

- Fuer die vollstaendige Versionshistorie siehe [PATCHNOTES.de.md](PATCHNOTES.de.md).

