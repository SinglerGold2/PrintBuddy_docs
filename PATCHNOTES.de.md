# Patchnotes

[🇬🇧 English Version](PATCHNOTES.md)

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

## Version 0.9.1 - 20.09.2026

### Änderungen

- Das Flackern der Multitool-IP im Property Inspector wurde behoben; Ursache waren wiederholte Settings-Schreibvorgänge, weil normalisierte `selectedExtruders`-Arrays per Referenz verglichen wurden.
- Der referenzbasierte Vergleich wurde durch einen wertbasierten Vergleich der normalisierten Multitool-Einstellungen ersetzt, um Save-Echo-Loops zu vermeiden.
- Zuverlässiges Verhalten beim Auswählen/Abwählen der Extruder in Lite und Pro wiederhergestellt, inklusive Auswahlreihenfolge, Labels und Maximum von vier Tools.
- Aktive Eingaben und dynamische Tool-Steuerelemente im Property Inspector bleiben bei Settings-Refresh erhalten.
- Multitool-Regressions-Tests ergänzt, die explizit keinen Netzwerkzugriff verwenden und das Persistenzverhalten der Auswahl absichern.

## Version 0.8.0 - 17.09.2026

### Änderungen

- Die Einstellungen für Status, Status FX und MultiExtruder wurden für eine leichtere Navigation in übersichtliche Tabs gegliedert.
- Die Status-FX-Gauge-Optionen wurden um eine datentypabhängige Sichtbarkeit, Temperaturbereiche, frei wählbare Farben und eine Farbe für Geschwindigkeit und Fluss über 100 % erweitert.
- Anordnung und Skalierung von Werten und Beschriftungen wurden für Ring-, Bogen- und Kreis-Gauges verbessert.
- Der leer erscheinende Tab „Anzeigeoptionen“ wurde behoben und das Speichern, erneute Öffnen sowie Wechseln von Themes zuverlässiger gemacht.
- Die neuen Tabs und Gauge-Einstellungen wurden vollständig in alle 12 unterstützten Sprachen übersetzt.

## Version 0.7.21 - 17.09.2026

### Änderungen

- Property-Inspector-Overrides für theme-vorgegebene `valueFontSize`- und `labelFontSize`-Werte aktiviert.
- Sichergestellt, dass manuelle Schriftgrößenänderungen auch bei Nicht-Benutzer-Preset-Themes erhalten bleiben.
- Einmalige Anwendung empfohlener Theme-Standardwerte beim Theme-Wechsel beibehalten.
- Die Auswahl „Button Style“ im Property Inspector ausgeblendet, während bestehende interne Bindings und das Classic-Fallbackverhalten erhalten bleiben.
- Runtime-Normalisierung, Property-Inspector-Persistenz und Rollup-Build erneut validiert.

## Version 0.7.7 - 16.09.2026

### Änderungen

- Preset-Theme-Laden in der Runtime korrigiert, indem die nicht Rollup-kompatible `import.meta.glob`-Erkennung in `src/core/themes/theme-registry.ts` durch explizite statische Imports ersetzt wurde.
- Sichergestellt, dass Nicht-Benutzer-Presets jetzt über Classic-, Neon-Glow- und Cyber-Button-Varianten hinweg ihre vollständige eigene Palette und Text-Defaults anwenden.
- Verhalten des Benutzer-Themes beibehalten, sodass benutzerdefinierte persistierte Property-Inspector-Werte editierbar und theme-lokal bleiben.
- TypeScript-, Build- und i18n-Audit-Pipeline erneut validiert und bestätigt, dass das generierte Bundle eindeutige Preset-Palette-/Text-Tokens enthält (z. B. Prusa, Klipper, Synthwave).

## Version 0.7.5 - 16.09.2026

### Änderungen

- Standard-Fallback auf Moonraker-Port `7125` ergänzt, wenn eine Adresse ohne expliziten Port konfiguriert ist.
- Lokalisierte Meldungen für fehlenden Port und ungültige Antworten in allen 12 aktiven Runtime- und Property-Inspector-Katalogen ergänzt, einschließlich beabsichtigter Zeilenumbrüche für 144x144-Tasten.
- Dynamische Text-Layout-Engine mit Auto-Fit, Umbruch, maximaler Zeilenzahl und begrenzter Höhe eingeführt.
- Den SVG-Textvertrag von Mittelpunkt- auf Oberkanten-Baselines korrigiert, wodurch vertikal verschobene oder abgeschnittene lokalisierte Meldungen verhindert werden.
- Zentralen `ButtonRenderer` für Hintergründe, Meldungstasten und Telemetrietext von PrintBuddy Status ergänzt; die bewährte 72x72-Komposition bleibt bei 144x144-Skalierung erhalten.
- Neutrale Hintergründe für die informativen Zustände „Fehlende IP“ und „Offline“ beibehalten und durchgängig lokalisierte Strings in den betroffenen Action-Pfaden sichergestellt.
- Build, TypeScript-Kompilierung, Baseline im generierten Bundle und i18n-Parität über 12 aktive Locales und 140 Referenzschlüssel validiert.

## Version 0.7.0 - 15.09.2026

### Änderungen

- Theme-Auflösung korrigiert: PrintBuddy bleibt die absolute Basis, Presets ersetzen die vollständige Palette und nur das Benutzer-Theme übernimmt individuelle Property-Inspector-Werte.
- Kanonisches `baseColor2` als Hintergrund-Farbstopp für Klassisch, Neon Glow und Cyber Tech ergänzt. Der ursprüngliche `baseColor_Cyber`-Wert `#0f1a2a` und der `baseColor_ring`-Standardwert `#39ff14` bleiben ausschliesslich für die Einstellungsmigration lesbar.
- Lineare und radiale Verlaufsrichtungen dynamisch angewendet, einschliesslich umgekehrter Farbstopps für `edge-to-center`.
- Den ursprünglichen harten Cyber-Tech-Hintergrund-Fallback `#000000` entfernt und das Matrix-Motiv als Overlay über dem aufgelösten Theme-Verlauf angeordnet.
- Kräftigere Cyber-Tech-Klammern über die volle Höhe mit Strichstärke `2.5` ergänzt. Die ursprüngliche Matrix-Overlay-Deckkraft `0.96` und Neon-Glow-Rahmenbreite `1.25` bleiben unverändert.
- Die ursprünglichen Richtungs-Fallbacks `top-right` und `center-to-edge` beibehalten und die Richtungsspeicherung nach Button-Stil getrennt.
- Die bisherigen `src/core/theme`-Kompatibilitäts-Wrapper entfernt und Consumer auf `src/core/themes` migriert.

## Version 0.6.7 - 15.09.2026

### Änderungen

- Klingon-Locale, Aliase, Übersetzungsoptionen und Flaggen-Asset entfernt.
- `src/core/i18n/active-locales.ts` als kanonische Liste der 12 unterstützten Locales eingeführt.
- Build-Generierung von `ui/shared/i18n-locales.js` aus den TypeScript-Runtime-Katalogen ergänzt.
- Property-Inspector-Lokalisierung mit schlüsselweisem `en_gb`-Fallback und arabischer RTL/LTR-Umschaltung überarbeitet.
- i18n-Audit um Locale-/Schlüsselparität, Flaggen-Assets, Bundle-Parität, Script-Reihenfolge und entfernte Locale-Referenzen erweitert.
- Fehlende Übersetzungen für Gradientenrichtungen in allen aktiven Katalogen ergänzt.
- Generische Core-Module in `action-settings.ts`, `i18n/localization.ts`, `themes/theme-registry.ts` und `graphics/styles/button-style-renderer.ts` umbenannt.

## Version 0.6.6 - 15.09.2026

### Änderungen

- Locale-Umschaltung für nicht-englische und nicht-deutsche Locale-Dateien durch vollständige statische Fallback-Loader im früheren Modul `src/core/i18n/index.ts` korrigiert.

## Version 0.6.5 - 15.09.2026

### Änderungen

- Entwicklungsumgebung und getestete Hardware-Geräte (Stream Deck MK.2, XL, Plus v1) dokumentiert, historische Release-Zeitstempel anhand von Git-Tag-Metadaten korrigiert und auf natives GitHub-Workflow-Status-Badge umgestellt.

## Version 0.6.4 - 15.09.2026

### Änderungen

- Patchnotes vervollständigt - Vollständige historische Release-Historie nachgepflegt.
- Build-Badges in allen Dokumenten auf die GitHub-Actions-Workflow-URL mit explizitem Branch main korrigiert.
- Release-Metadaten und Versionsverweise auf 0.6.4 synchronisiert.

## Version 0.6.3 - 15.09.2026

### Änderungen

- Behebung der Property-Inspector-Flaggenpfadauflösung für alle 13 unterstützten Sprachen.
- Strikte Locale-Normalisierung auf Kleinschreibung mit Unterstrich zur Vermeidung von PI-404-Fehlern.
- Entfernung harter Sprachlisten und dynamische Registrierung der Locale-Optionen aus geladenen Übersetzungen.
- Sofortige Neuübersetzung aller data-i18n gebundenen PI-Elemente beim Sprachwechsel sichergestellt.
- PI-Footer-Versionsanzeige mit Build- und Manifest-Releaseversion v0.6.3 synchronisiert.
- Englische JSDoc-Abdeckung über JS- und TS-Funktionen, Methoden und Klassen erweitert.
- Standardisierten visuellen HTML-Header in alle Release- und Projekt-Markdown-Dateien integriert.

## Version 0.6.2 - 14.09.2026

### Änderungen

- Repository-Dokumentation über alle Markdown-Dateien hinweg aktualisiert und standardisiert.

## Version 0.6.1 - 14.09.2026

### Änderungen

- Zweisprachige Dokumentationsarchitektur über alle Repository-Markdown-Dateien standardisiert.
- Öffentliche Dokumentation von internen Build-Validierungsprotokollen bereinigt.
- Projektstatus und Versionierung auf 0.6.1 synchronisiert.

## Version 0.6.0 - 14.09.2026

### Änderungen

- Runtime-i18n auf echtes Lazy Loading mit asynchronem Nachladen pro Locale und Cache umgestellt.
- Locale- und Flag-Namensschema auf ISO-Underscore vereinheitlicht.
- Automatische Build-Metadaten und DIN-5008-Zeitstempel-Footer für alle Property Inspectoren ergänzt.

## Version 0.5.17 - 14.09.2026

### Änderungen

- Locale- und Flag-Namenskonventionen in Runtime und PI auf ISO-Underscore standardisiert.

## Version 0.5.16 - 14.09.2026

### Änderungen

- Dynamische Locale-Registry und PI-Flaggenhandling für mehrsprachige Property-Inspectoren umgesetzt.

## Version 0.5.15 - 13.09.2026

### Änderungen

- Neon-Radial-Gradientenrichtung und style-spezifische Gradientenzuordnung korrigiert.

## Version 0.5.11 - 13.09.2026

### Änderungen

- Patchnotes-Tracking ergänzt und Release-Metadaten auf 0.5.11 synchronisiert.

## Version 0.5.10 - 14.09.2026

### Änderungen

- Markdown-Dokumentation und Release-Versionsmetadaten synchronisiert.

## Version 0.5.7 - 14.09.2026

### Änderungen

- Zentrale Locale-zu-Flag-Mapping-Logik und dynamische PI-Sprachauswahl für alle unterstützten Sprachen ergänzt.

## Version 0.5.6 - 14.09.2026

### Änderungen

- Netzwerk- und IP-Persistenzverantwortung in geschützte Core-Modulgrenzen überführt.
- Dokumentation und Release-Metadaten synchronisiert.

## Version 0.5.4 - 14.09.2026

### Änderungen

- Englische JSDoc-Header und Release-Dokumentationsmetadaten standardisiert.

## Version 0.5.3 - 14.09.2026

### Änderungen

- Markdown-Dokumentation und Release-Synchronisierungstexte aktualisiert.

## Version 0.5.2 - 14.09.2026

### Änderungen

- Projektdokumentationssatz aktualisiert und Release-Metadaten synchronisiert.

## Version 0.5.1 - 14.09.2026

### Änderungen

- Frühe Release-Basis für modularen Runtime- und Dokumentationsfluss etabliert.

## Version 0.1.1 - 14.09.2026

### Änderungen

- Erstes Wartungsrelease nach der initialen öffentlichen Versionsbasis durchgeführt.

## Version 0.1.0 - 14.09.2026

### Änderungen

- Erster formaler semantischer Versionssprung auf 0.1.0 eingeführt.
