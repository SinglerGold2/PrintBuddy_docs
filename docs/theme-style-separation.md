# Theme/Style Separation

[🇩🇪 Deutsche Version](theme-style-separation.de.md)

Version reference: `0.9.2`

## Goal

Ensure layout rendering (button style) and visual palette (theme) are cleanly separated.

## Architecture summary

- Dedicated renderer contract in `src/core/graphics/styles/types.ts`.
- Registry-based style resolution and rendering dispatch in `src/core/graphics/styles/button-style-renderer.ts`.
- Theme presets provide palette/text defaults only and do not override style selection.
- Theme preset aggregation lives in `src/core/themes/theme-registry.ts`.
- Theme IDs, labels, palettes, and rendering overrides live in runtime-loaded `com.ulli.printbuddy.sdPlugin/themes/*.theme.json` files. Pro additionally loads user themes from `com.ulli.printbuddy.sdPlugin/themes/userthemes`; generated Property Inspector defaults use the bundled JSON files.
- Runtime consumers import directly from the canonical `themes` domain; the former `src/core/theme/` compatibility wrappers have been removed.
- Action setting normalization is provided by `src/core/action-settings.ts`.
- `src/core/render/ButtonRenderer.ts` composes the resolved style background with message or telemetry text; it consumes resolved settings but does not own theme selection or style definitions.
- Text fitting remains a rendering concern in `src/core/graphics/text-engine.ts`, while SVG serialization in `src/core/render/text-render.ts` preserves the resulting top-edge coordinates.
- PrintBuddy is the absolute base theme. A selected preset replaces the complete palette. Only `USER_THEME`, including the legacy input alias `custom`, applies individual Property Inspector values.
- `baseColor` and `baseColor2` are the only primary button background gradient stops. Style renderers add transparent visual layers without repurposing `baseColor2` as a border or accent.
- Classic and Cyber Tech use their resolved linear direction. Neon Glow uses its resolved radial direction and reverses colour stops for `edge-to-center`.
- Theme palettes are frozen in the registry, and palette resolution returns a fresh object to prevent consumer mutation.
- Theme definitions are statically imported in the registry to remain Rollup-compatible and guarantee that all presets are present in runtime bundles.
- Property Inspector theme values remain editable and persist independently from the selected preset; changing a theme applies its recommended defaults once.

## Migration values

- The original `baseColor_Cyber` key and its PrintBuddy value `#0f1a2a` were replaced by canonical `baseColor2`. Existing settings using the original key are still read during migration.
- The original `baseColor_ring` key and its default value `#39ff14` were replaced by `baseColor2` in Property Inspector payloads. Existing settings using the original key are still read during migration.
- The original Cyber Tech hard fallback `#000000` was removed. Its background now always uses the resolved theme gradient.
- The original matrix overlay opacity `0.96` remains unchanged. The original outer Neon Glow border width `1.25` remains unchanged.
- Cyber Tech now adds full-height brackets with a `2.5` stroke width. The previous matrix artwork did not guarantee full-height bracket coverage.
- Original direction fallbacks remain `top-right` for linear gradients and `center-to-edge` for Neon Glow.

## Result

- Predictable behavior when switching style and theme independently.
- Backward-compatible rendering API.
- Descriptive module filenames replace ambiguous `index.ts` and `settings.ts` names.
- PrintBuddy Status now shares one 144x144 composition path for regular telemetry and localized connection messages without merging theme, style and text-layout responsibilities.

