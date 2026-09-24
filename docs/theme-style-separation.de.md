# Theme/Style-Trennung

[🇬🇧 English Version](theme-style-separation.md)

Versionsbezug: `0.9.2`

## Ziel

Eine saubere Trennung zwischen Layout-Rendering (Button-Style) und visueller Farbpalette (Theme) sicherstellen.

## Architekturüberblick

- Eigener Renderer-Vertrag für Button-Styles in `src/core/graphics/styles/types.ts`.
- Registry-basierte Auflösung und Ausführung der Style-Renderer in `src/core/graphics/styles/button-style-renderer.ts`.
- Theme-Presets liefern nur Farb-/Textdefaults und überschreiben keine Style-Auswahl.
- Die Theme-Preset-Aggregation befindet sich in `src/core/themes/theme-registry.ts`.
- Theme-IDs, Labels, Paletten und Rendering-Overrides liegen in zur Laufzeit geladenen `com.ulli.printbuddy.sdPlugin/themes/*.theme.json`-Dateien. Pro lädt zusätzlich Benutzer-Themes aus `com.ulli.printbuddy.sdPlugin/themes/userthemes`; die generierten Property-Inspector-Defaults verwenden die mitgelieferten JSON-Dateien.
- Runtime-Consumer importieren direkt aus der kanonischen `themes`-Domäne; die früheren Kompatibilitäts-Wrapper unter `src/core/theme/` wurden entfernt.
- Die Normalisierung von Action-Einstellungen erfolgt in `src/core/action-settings.ts`.
- `src/core/render/ButtonRenderer.ts` kombiniert den aufgelösten Style-Hintergrund mit Meldungs- oder Telemetrietext; er verwendet aufgelöste Einstellungen, übernimmt aber weder Theme-Auswahl noch Style-Definitionen.
- Die Textanpassung bleibt eine Rendering-Verantwortung in `src/core/graphics/text-engine.ts`, während die SVG-Serialisierung in `src/core/render/text-render.ts` die resultierenden Oberkanten-Koordinaten beibehält.
- PrintBuddy ist das absolute Basis-Theme. Ein ausgewähltes Preset ersetzt die vollständige Palette. Nur `USER_THEME`, einschliesslich des bisherigen Eingabe-Alias `custom`, übernimmt individuelle Werte aus dem Property Inspector.
- `baseColor` und `baseColor2` sind die einzigen Farbstopps des primären Button-Hintergrundverlaufs. Style-Renderer ergänzen transparente visuelle Ebenen, ohne `baseColor2` als Rahmen- oder Akzentfarbe zu verwenden.
- Klassisch und Cyber Tech verwenden ihre aufgelöste lineare Richtung. Neon Glow verwendet seine aufgelöste radiale Richtung und kehrt für `edge-to-center` die Farbstopps um.
- Theme-Paletten sind in der Registry eingefroren und die Auflösung liefert eine neue Objektkopie, damit Consumer keine Registry-Daten verändern.
- Theme-Definitionen werden in der Registry statisch importiert, um Rollup-kompatibel zu bleiben und sicherzustellen, dass alle Presets in Runtime-Bundles vorhanden sind.
- Theme-Werte bleiben im Property Inspector unabhängig vom gewählten Preset bearbeitbar und gespeichert; ein Theme-Wechsel wendet die empfohlenen Defaults einmalig an.

## Migrationswerte

- Der ursprüngliche Schlüssel `baseColor_Cyber` und sein PrintBuddy-Wert `#0f1a2a` wurden durch das kanonische `baseColor2` ersetzt. Vorhandene Einstellungen mit dem ursprünglichen Schlüssel werden bei der Migration weiterhin gelesen.
- Der ursprüngliche Schlüssel `baseColor_ring` und sein Standardwert `#39ff14` wurden in Property-Inspector-Payloads durch `baseColor2` ersetzt. Vorhandene Einstellungen mit dem ursprünglichen Schlüssel werden bei der Migration weiterhin gelesen.
- Der ursprüngliche harte Cyber-Tech-Fallback `#000000` wurde entfernt. Der Hintergrund verwendet jetzt immer den aufgelösten Theme-Verlauf.
- Die ursprüngliche Deckkraft `0.96` des Matrix-Overlays bleibt unverändert. Die ursprüngliche äussere Neon-Glow-Rahmenbreite `1.25` bleibt unverändert.
- Cyber Tech ergänzt jetzt Klammern über die volle Höhe mit einer Strichstärke von `2.5`. Das bisherige Matrix-Motiv garantierte keine Klammerdarstellung über die volle Höhe.
- Die ursprünglichen Richtungs-Fallbacks bleiben `top-right` für lineare Verläufe und `center-to-edge` für Neon Glow.

## Ergebnis

- Vorhersehbares Verhalten beim unabhängigen Wechsel von Style und Theme.
- Rückwärtskompatible Rendering-API.
- Eindeutige Moduldateinamen ersetzen mehrdeutige `index.ts`- und `settings.ts`-Namen.
- PrintBuddy Status verwendet jetzt einen gemeinsamen 144x144-Kompositionspfad für reguläre Telemetrie und lokalisierte Verbindungsmeldungen, ohne Theme-, Style- und Textlayout-Verantwortlichkeiten zu vermischen.

