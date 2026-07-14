# Design System Documentation: The Precision Engine

## 1. Overview & Creative North Star
This design system is built for the power user—the developer who treats their keyboard as an instrument. Our Creative North Star is **"The Precision Engine."** 

Unlike generic productivity tools that rely on soft roundness and "friendly" whitespace, this system embraces the aesthetic of high-end code editors and terminal emulators. We move beyond the "template" look by utilizing aggressive tonal layering, intentional asymmetry, and a high-contrast technical palette. The goal is to create an environment that feels efficient, low-latency, and architecturally sound. We replace structural lines with depth, and generic buttons with tactile, high-contrast triggers.

---

## 2. Colors & Surface Philosophy
The palette is rooted in a deep, atmospheric obsidian, punctuated by "Rust" (Primary) and "Teal" (Secondary) accents that serve as functional beacons.

### The "No-Line" Rule
**Strict Mandate:** Traditional 1px solid borders are prohibited for sectioning. We define space through "chromatic architecture." Use background shifts to separate the sidebar from the main stage. 
- Use `surface_container_low` (#1C1B1B) for the main background.
- Use `surface_container` (#201F1F) for secondary navigation panels.
- Use `surface_container_high` (#2A2A2A) for active workspace areas.

### Surface Hierarchy & Nesting
Think of the UI as a series of machined plates stacked on top of each other.
- **Level 0 (Base):** `surface` (#131313) for the outermost application shell.
- **Level 1 (Panels):** `surface_container_low` for large content areas.
- **Level 2 (Interactive):** `surface_container_highest` (#353534) for cards or input zones.
This nesting creates a "tactile" depth that guides the eye without the visual noise of dividers.

### The Glass & Gradient Rule
For floating elements (modals, command palettes, or tooltips), use a "Frosted Terminal" effect. Use `surface_container_high` at 80% opacity with a `24px` backdrop blur. 
**Signature CTA Texture:** For primary actions, apply a subtle linear gradient from `primary` (#FFB59D) to `primary_container` (#EE6737) at a 135-degree angle. This adds a "glowing filament" quality to the technical dark theme.

---

## 3. Typography
The typographic system balances the geometric authority of **Space Grotesk** with the high-legibility precision of **Inter**.

- **Display & Headlines (Space Grotesk):** These are your "Editorial" moments. Use `display-md` or `headline-lg` for dashboard summaries. The wide apertures of Space Grotesk feel engineered and modern.
- **The Shortcut Monospace:** While not explicitly in the token list, all "Key" elements (Cmd, Shift, P) must be rendered in a monospaced typeface (e.g., JetBrains Mono or similar) using the `label-md` or `label-sm` scale. This distinguishes "data" from "action."
- **Body & Titles (Inter):** Use `body-md` for descriptions and `title-sm` for settings. Inter provides the neutral, Swiss-style clarity required for complex data tables.

---

## 4. Elevation & Depth
In this design system, elevation is a product of light and tone, not shadows alone.

- **The Layering Principle:** Achieve lift by placing a `surface_container_highest` object on a `surface_container_low` background. The contrast in value creates a natural "step up."
- **Ambient Shadows:** For floating command palettes, use an ultra-diffused shadow: `0px 20px 40px rgba(0, 0, 0, 0.4)`. The shadow color should never be pure black; it should feel like an occlusion of the `surface` color.
- **The Ghost Border Fallback:** If a boundary is required for accessibility (e.g., an input field), use the "Ghost Border." Apply `outline_variant` (#58413A) at 20% opacity. It should be felt, not seen.

---

## 5. Components

### Shortcut Keys (KBD)
The core atom of the app.
- **Style:** Use `surface_container_highest` background. 
- **Shape:** `sm` corner radius (0.125rem) to maintain a sharp, technical look.
- **Typography:** Monospaced `label-md` using `on_surface_variant` (#E0BFB6).
- **Detail:** A 1px bottom "shim" of `outline` (#A78A81) at 30% opacity to simulate key height.

### Primary Buttons
- **Style:** Gradient fill (`primary` to `primary_container`).
- **Typography:** `label-md` in `on_primary` (#5D1800), bold weight.
- **Interaction:** On hover, increase the `surface_tint` overlay by 10% to create a "charging" effect.

### Data Tables (The "Terminal" Grid)
- **Rules:** No vertical or horizontal lines.
- **Separation:** Use `surface_container_low` for the header row and alternating `surface_container_lowest` for rows.
- **Hover State:** Highlight the entire row with `surface_container_highest` and a `secondary` (#4FDBC8) 2px left-accent "indicator" strip.

### Input Fields
- **Style:** Minimalist. No background fill—only a `surface_container_highest` bottom border (2px).
- **Focus State:** The bottom border transitions to `secondary` (#4FDBC8) with a soft outer glow.

---

## 6. Do’s and Don’ts

### Do
- **Do** use `secondary` (#4FDBC8) for "Success" states and active system status indicators.
- **Do** lean into asymmetry. For example, a sidebar can be significantly narrower than a standard 240px grid if the icons are high-contrast.
- **Do** use `tertiary` (#79D1FF) for "Information" or "Documentation" links to separate them from functional shortcuts.

### Don't
- **Don't** use `DEFAULT` or `xl` roundedness for primary containers. Keep the interface "sharp" using `sm` (0.125rem) or `none`. Reserve `full` only for status pips.
- **Don't** use pure white for text. Always use `on_surface` (#E5E2E1) to reduce eye strain in dark environments.
- **Don't** use standard "Drop Shadows" on cards. If a card needs to stand out, change its background token to a higher tier (e.g., from `low` to `high`).

---

## 7. Implementation Note: Tonal Continuity
When building complex views, ensure that the most "interactive" elements are always the brightest/highest in the tonal stack. If a user is editing a shortcut, that specific input row should shift to `surface_bright` (#3A3939) to signal focus, while the rest of the table dims to `surface_dim` (#131313).