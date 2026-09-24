# PrintBuddy

## Provider-Integration (v0.10.6)

Pro und Lite bieten in allen enthaltenen Property Inspectors **Klipper / Moonraker** (Standard für bestehende Profile), **lokales PrusaLink v1** und **Bambu LAN (local)**. Die Provider-Auswahl ist kein Editionsunterschied. Für Bambu LAN die lokale Druckeradresse, Seriennummer und den LAN-Zugriffscode eingeben; die Prüfung am echten Drucker steht noch aus. Für PrusaLink die lokale Druckeradresse und entweder einen API-Schlüssel (sofern von der Firmware unterstützt) oder PrusaLink-Benutzername/Passwort für HTTP Digest eingeben. Ein API-Schlüssel hat Vorrang. Keine Prusa-Connect-Cloud-Zugangsdaten verwenden.

- Prusa-Status: Düsen-/Betttemperatur, Fortschritt, Zustand, Dateiname, Restzeit, Z-Position, Geschwindigkeit/Fluss und Drucklüfter-RPM, soweit die Firmware diese liefert. Polling mindestens einmal pro Sekunde und Action, fünf Sekunden Request-Timeout, automatische Wiederverbindung.
- Prusa-Steuerung: **Pause, Fortsetzen, Druckabbruch**. Abbruch behält die Haltebestätigung. **Not-Aus wird nicht auf Druckabbruch umgebogen.** Licht, Speed Dial und freier G-Code sind nicht verfügbar.
- MultiExtruder zeigt die gemeldete aktuelle Düse in T0. Die Zuordnung einzelner XL-Werkzeuge ist nicht implementiert oder verifiziert; weitere Plätze zeigen unbekannte Werte. Das ist eine Integrationsgrenze, keine Aussage über technische Unmöglichkeit.
- Prusa-Webcams benötigen eine explizite, separat erreichbare Snapshot-URL. Drucker-Zugangsdaten werden niemals an Webcam-Hosts weitergegeben.
- Zugangsdaten liegen in Stream-Deck-Action-Einstellungen, nicht in einem verschlüsselten Tresor. Profile nicht mit Geheimnissen exportieren; möglichst HTTPS oder ein vertrauenswürdiges lokales Netzwerk verwenden. Redirects werden abgewiesen, TLS-Prüfung bleibt aktiv.
- Alte PrusaLink-Firmware nur mit `/api/printer` und Prusa Connect Cloud sind nicht implementiert oder verifiziert. Provider-Hinweise sind in allen 13 Sprachen übersetzt. Bei Benutzername/Passwort den API-Schlüssel leer lassen; Zugangsdaten am Drucker unter Einstellungen → Netzwerk → PrusaLink.
- Jobdetails sind optional: Fehlende Details, Netzwerkfehler und Detail-Timeouts erhalten den aktuellen Basisstatus. Anmeldefehler und ausdrücklicher Abbruch werden nicht verschluckt. Nur übereinstimmende Job-IDs werden zusammengeführt; alte Dateinamen und Messwerte werden nicht zwischen Abfragen behalten. Endliche Zahlenstrings werden akzeptiert; nur der Fortschritt wird auf 0–100 % begrenzt (nicht Geschwindigkeit/Fluss). Fehlender Fortschritt bleibt unbekannt.

Technische Referenz: [Gantrybar-Quellenangabe und MIT-Hinweis](com.ulli.printbuddy.sdPlugin/THIRD-PARTY-NOTICES.md), mit festgelegter Revision und Bestandteil beider Pro-/Lite-Distributionen. Zusätzliche Prusa-Befehle bleiben unimplementiert/unverifiziert und werden durch diese Referenz nicht freigeschaltet.

Prüfung: `npm run test:providers`, bestehende Steuerungs-/Status-/Webcam-/MultiExtruder-/Theme-Tests, TypeScript und Pro-/Lite-Builds. Tests mit echtem Drucker und der Stream-Deck-Oberfläche bleiben vor Freigabe erforderlich.

[🇬🇧 English Version](README.md)

## Template-Logos (v0.10.0)

Anycubic, Bambu Lab, Creality, Elegoo, Elgato, FlashForge, Fluidd, Klipper,
OctoPrint, Prusa, Snapmaker und Voron verwenden nun passende,
einfärbbare SVG-Hintergrundlogos. Ohne Logo-Zuordnung bleibt die bisherige
Action-Darstellung erhalten. Unter **User Theme → Template-Logo** stehen Auswahl,
Farbe, Deckkraft und Größe bereit; in Pro speichert **Save as…** die Zuordnung
als eigenes Theme. Feste Templates werden über ihre JSON-Datei konfiguriert.
Control-Funktionssymbole bleiben im Vordergrund, Webcam-Snapshots unverändert.

Die [SVG-/Theme-Anleitung](com.ulli.printbuddy.sdPlugin/themes/README.md) erklärt
`currentColor`, `viewBox`, Größenverhalten und die Registrierung weiterer Logos.
Quellen: allsvgicons.com und svgrepo.com. Einzelne Lizenznachweise sind noch offen;
siehe [Drittanbieterhinweise](com.ulli.printbuddy.sdPlugin/THIRD-PARTY-NOTICES.md).
Regressionstest: `npm run test:logos`.

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

Stream-Deck-Plugin zur Überwachung und Steuerung von 3D-Druckern (Fokus: Klipper/Moonraker).

**Aktuelle Version:** `0.10.6`

## Changelog (v0.10.6)

- Synchronisierte Lite/Pro-Auslieferung verbindlich gemacht: gemeinsamer Workflow für `build`/`build:lite`/`build:pro` plus Paritätsprüfungen für Versionen, Manifeste, gemeinsame UI/Provider und erlaubte Editionsunterschiede.
- Alle gebündelten Theme-JSON-Dateien mit einheitlicher Formatierung normalisiert und ein garantiertes `logo`-Objekt ergänzt (`id: "none"` als Fallback ohne Logo-Zuordnung).
- JSON-kompatible Theme-Metadaten (`_header`, `_comment`) sowie `_ipNotice` in gebrandeten/Logo-Themes ergänzt; Metadaten-Texte auf Englisch vereinheitlicht.
- Theme-Paritätsprüfung auf Vergleich von geparstem JSON statt Rohtext gehärtet, damit reine Formatänderungen keine Fehlalarme auslösen.
- Lokale Validierung erfolgreich mit `npm run build`, `npm run test:logos` und `npm run test:editions`; abschließend steht nur die Bambu-LAN-Hardwareprüfung am echten Gerät aus.

## Changelog (v0.10.0)

- Gemeinsame Provider-Integration für lokales PrusaLink v1 (API-Key oder Digest-Auth) in allen Property Inspectors für Pro und Lite ergänzt, Moonraker bleibt Standard.
- Einfärbbare Template-Logo-Pipeline ergänzt und auswählbare Logo-IDs auf Anycubic, Bambu Lab, Creality, Elegoo, Elgato, FlashForge, Fluidd, Klipper, OctoPrint, Prusa, Snapmaker und Voron erweitert.
- Workflow für Logo-Quellen/Aufbereitung/Tests (`assets/logo-sources` → `scripts/prepare-theme-logos.mjs` → `imgs/logos`) sowie Theme- und Rechtshinweise aktualisiert.

## Changelog (v0.9.2)

- Risiko-/Fehlfunktionen für Theme-Dateiaktionen im Property Inspector entfernt; es bleibt nur der sichere Theme-Datei-Flow.
- Theme-Dateiaktionen zeigen jetzt nur noch **Save as…** (`themes:save`) und **Reload** (`themes:reload`).
- Backend-Verarbeitung für den obsoleten Befehl **Open folder** entfernt.
- User-Theme-Dokumentation um Save/Reload-Workflow, Namensregeln, JSON-Struktur und Validierungsregeln erweitert.

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
- `npm run build`: baut Quell-Plugin, Lite und Pro gemeinsam und prüft danach die Editionsparität.
- `npm run build:lite` / `npm run build:pro`: Kompatibilitäts-Aliase für denselben gemeinsamen Build; keine einseitigen Updates.
- `npm run test:editions`: prüft die vorhandenen Builds auf gleiche Version/Zeitstempel, aktuelle gemeinsame UI-Dateien, alle drei Provider und erlaubte Manifest-/Theme-Unterschiede.
- `npm run watch`: aktualisiert alle drei Build-Ziele; nach erfolgreicher Paritätsprüfung werden Lite und Pro neu gestartet.

**Verbindliche Editionsregel:** Lite und Pro bleiben immer auf demselben Quell-, Versions- und gemeinsamen Funktionsstand. Unterschiede sind nur im vorab vereinbarten Umfang erlaubt (bestehende Status-FX-, Theme-/Anpassungs- und Extrudergrenzen); neue Unterschiede müssen vorab abgestimmt werden. Bambu LAN ist in beiden Editionen verfügbar. Stream Deck muss auf die passenden `dist/lite`- bzw. `dist/pro`-Pluginordner verweisen; ein Git-Push allein aktualisiert keine Installation.

## Drittanbieter-Assets

- Icon-Attribution: `com.ulli.printbuddy.sdPlugin/licences/ICON_ATTRIBUTION.de.md`

## Vollstaendige Release-Historie

- Fuer die vollstaendige Versionshistorie siehe [PATCHNOTES.de.md](PATCHNOTES.de.md).

