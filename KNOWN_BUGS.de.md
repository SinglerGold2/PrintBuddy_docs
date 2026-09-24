# Bekannte Bugs

[🇬🇧 English Version](KNOWN_BUGS.md)

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

Stand: 24.09.2026
Version: `0.10.6`

## Kritisch

_Keine bekannten kritischen Bugs._

## Hoch

_Keine bekannten Bugs mit hoher Priorität._

## Mittel

### Physische Stream-Deck-Prüfung noch offen

- **Problem:** Die manuelle Geräteprüfung ist noch offen; aktuell ist kein reproduzierbarer Fehler bekannt.
- **Betroffener Bereich:** Stabilität der Multitool-IP-Eingabe im Property Inspector, Lite/Pro-Extruder-Auswahl/Abwahl, Auswahlreihenfolge, Labels und Vier-Tool-Limit.
- **Erwartetes Verhalten:** Die IP-Eingabe bleibt beim Tippen stabil; Extruder-Auswahlen bleiben korrekt erhalten, ohne unbeabsichtigte Resets oder Reihenfolgewechsel.
- **Aktueller Stand:** Regressions-Tests sind erfolgreich, Code-Fixes sind umgesetzt; die interaktive Hardware-Prüfung läuft aktuell.
- **Reproduzierbarkeit:** N/A (Validierungsaufgabe)
- **Priorität:** Mittel
- **Status:** Offen

## Niedrig

_Keine bekannten Bugs mit niedriger Priorität._

## Vollstaendige Release-Historie

- Fuer die vollstaendige Versionshistorie siehe [PATCHNOTES.de.md](PATCHNOTES.de.md).

