# PrintBuddy theme files

Version reference: `0.10.6`

PrintBuddy loads every `*.theme.json` file in this directory at startup. Pro also
loads user files from `themes/userthemes` inside the plugin directory; a user file with the same
`name` replaces the bundled theme until that file is removed or becomes invalid.

The `themes/userthemes` folder is versioned with a placeholder file (`.gitkeep`) so
the directory always exists after install/checkout, even before the first saved user theme.

Required fields:

- `schemaVersion`: currently `1`
- `name`: uppercase identifier ending in `_THEME`
- `label`: display name (maximum 80 characters)
- `palette`: all palette properties shown in the bundled examples

Colors use six-digit hex notation (`#rrggbb`). `textBackgroundOpacity` is between
`0` and `1`. Optional `text` and `statusImage` objects override text/icon defaults.
Malformed files are ignored and PrintBuddy safely falls back to the bundled theme
or `PRINTBUDDY_THEME`.

## Tintable background logos

Optional theme field (old files without it retain the action icon):

```json
"logo": {
  "id": "prusa",
  "color": "#ffffff",
  "opacity": 0.1,
  "size": 60
}
```

IDs: `none`, `anycubic`, `bambulab`, `creality`, `elegoo`, `elgato`, `flashforge`, `fluidd`, `klipper`, `octoprint`, `prusa`, `snapmaker`, `voron`.
`none` means **no template logo**, not “hide the action icon”. Missing logo assets
also fall back to the original action artwork. Color is six-digit hex, opacity
is 0–1 and size is 16–64 in the button's 72 × 72 coordinate system (automatically
scaled for the 144 × 144 Status renderer). Artwork is centered without distortion.

In the Property Inspector, select **User Theme**, choose the logo, color, opacity
and size, then use **Save as…** in Pro to store the assignment in a theme file.
Fixed themes take their logo from JSON, not stale per-action settings; developers
can edit the bundled JSON and reload themes/restart the plugin. PrintBuddy has no
logo assignment. The six matching brand themes do. The dropdown does not edit a
bundled template in place. Lite uses its bundled themes and has no Save as feature.

Status/Status FX show the logo behind text, MultiTool behind its grid. Connecting,
offline and error artwork uses the logo instead of the action icon. Control keeps
its operational pause/resume/etc. symbol in front of the background logo so the
button remains identifiable. Webcam snapshots and its theme-free inspector are
unchanged. A logo does not affect printer commands, polling or touch behavior.

### Preparing an SVG as a developer

1. Keep a meaningful `viewBox`. Convert text to paths; do not depend on fonts.
2. Use `fill="currentColor"` for filled shapes, or `fill="none"` and
   `stroke="currentColor"` for outlines. Preserve `fill="none"`! Remove hardcoded
   fill/stroke colors, CSS paint overrides and fixed internal opacity if the
   theme should control them. No opaque background rectangle.
3. Use self-contained vector paths/groups. No scripts, event handlers, external
   URLs, embedded images, `foreignObject`, animation or network dependencies.
4. Place reviewed source SVGs in `assets/logo-sources/<id>.svg` and run
   `node scripts/prepare-theme-logos.mjs` to generate the distributable copies
   in `imgs/logos/<id>.svg`. Register new IDs in `src/core/themes/types.ts` and
   the dropdown/validation in `ui/shared/theme-controls.js`. Arbitrary file paths
   and SVG uploads are not accepted from theme JSON.
5. `prepare-theme-logos.mjs` is a converter for reviewed files, **not** a
   general-purpose sanitizer for untrusted SVG uploads.
6. The renderer substitutes `currentColor` before embedding the SVG as a data
   image. Theme opacity applies to the whole image. `preserveAspectRatio` fits it
   within the configured square. Adjust whitespace via the source `viewBox`;
   test at real Stream Deck size, including zero opacity and light/dark colors.
7. Record the original asset page, author, license and modifications in
   `THIRD-PARTY-NOTICES.md` before redistribution. Site provenance alone is not
   license clearance.

### Kurzfassung (DE)

Unter **User Theme → Template-Logo** das Logo, die Farbe, Deckkraft und Größe
wählen. **Kein Logo** behält die bisherige Action-Darstellung. Mit **Save as…**
in Pro wird die Zuordnung im Theme gespeichert. Feste Templates werden als
Entwickler über das obige `logo`-Objekt in ihrer JSON-Datei konfiguriert.
Für einfärbbare SVGs `currentColor` statt fester Farben verwenden; `fill="none"`
bei Liniengrafiken unbedingt erhalten. Ein korrektes `viewBox`, reine Pfade und
keine externen Ressourcen verwenden. Größe und Deckkraft steuert das Theme,
nicht die Druckerfunktion. Control-Funktionssymbole bleiben im Vordergrund.
