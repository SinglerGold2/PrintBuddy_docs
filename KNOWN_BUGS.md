# Known Bugs

[🇩🇪 Deutsche Version](KNOWN_BUGS.de.md)

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

Status date: 20.09.2026
Version: `0.9.1`

## Critical

_No known critical bugs._

## High

_No known high-priority bugs._

## Medium

### Physical Stream Deck verification still pending

- **Issue:** Manual on-device verification remains open; no reproducible defect is currently known.
- **Affected area:** Multitool Property Inspector IP entry stability, Lite/Pro extruder selection/deselection behavior, selection ordering, labels and the four-tool limit.
- **Expected behavior:** IP input remains stable while typing; extruder choices persist correctly without unintended resets or order changes.
- **Current behavior:** Regression tests pass and code-level fixes are in place; interactive hardware verification is currently in progress.
- **Reproducibility:** N/A (validation task)
- **Priority:** Medium
- **Status:** Open

## Low

_No known low-priority bugs._

## Full Release History

- For the complete version history, see [PATCHNOTES.md](PATCHNOTES.md).
