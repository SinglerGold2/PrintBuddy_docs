# PrintBuddy Pro user themes

Build metadata: `20260923.1101`  
Version: `0.10.6`  
Build: `0.10.6`

This folder is used by **PrintBuddy Pro** for custom theme files saved from the Property Inspector.

## Safe workflow in Property Inspector

Only these two actions are supported:

- **Save as…** → writes a validated `*.theme.json` file to this folder
- **Reload** → reloads theme files from disk and refreshes theme selection

Unsupported/risky file actions are intentionally not exposed.

## File naming

- File extension must be `.theme.json`
- Recommended lowercase filename, e.g. `blubbi.theme.json`
- Internal JSON `name` should end with `_THEME`, e.g. `BLUBBI_THEME`

## Minimal JSON structure

```json
{
  "schemaVersion": 1,
  "name": "BLUBBI_THEME",
  "label": "Blubbi",
  "palette": {
    "baseColor": "#20242b",
    "baseColor2": "#1a1f25",
    "textColor": "#e8ecf1"
  }
}
```

## UI setting → JSON mapping (high-level)

- Theme label/name fields → `label`, `name`
- Colour pickers → corresponding `palette` colour fields
- Text visibility/appearance options → `text` object fields (if set)
- Status image options → `statusImage` object fields (if set)

## Colour and validation rules

- Colours must be 6-digit hex format: `#rrggbb`
- Invalid JSON or schema violations are ignored safely
- On invalid file content, PrintBuddy falls back to bundled theme values

## Notes

- This folder is preserved in Pro rebuild workflows.
- Keep backups of your custom theme files before plugin updates.