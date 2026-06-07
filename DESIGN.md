---
colors:
  zinc:
    surfaces:
      page: "#09090b"
      panel: "#111113"
      card: "#17191e"
      sidebar: "#101216"
    text:
      high: "#fafafa"
      normal: "#f4f4f5"
      muted: "#a1a1aa"
      disabled: "#52525b"
      inverse: "#09090b"
    borders:
      default: "#27272a"
      strong: "#3f3f46"
      focus: "#60a5fa"
    focus:
      ring: "#60a5fa"
      ring_soft: "#93c5fd"
      background: "#172554"
    semantic:
      primary: "#3b82f6"
      success: "#22c55e"
      warning: "#f59e0b"
      danger: "#ef4444"
      info: "#06b6d4"
      muted: "#93a3b8"
    notes:
      surface_state: "Use neutral zinc surfaces before adding semantic overlays."
      text_role_priority: "Primary > secondary > muted > disabled."
typography:
  font_family:
    sans: "Inter, system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif"
    mono: "JetBrains Mono, ui-monospace, SFMono-Regular, Menlo, monospace"
  scale:
    xs: "0.75rem"
    sm: "0.875rem"
    base: "1rem"
    md: "1.125rem"
    xl: "1.25rem"
    xxl: "1.5rem"
    xxxl: "1.875rem"
  line_height:
    tight: "1.2"
    normal: "1.5"
    relaxed: "1.75"
  weight:
    light: "300"
    normal: "400"
    medium: "500"
    semibold: "600"
    bold: "700"
  tracking:
    normal: "0"
spacing:
  compact: "0.125rem"
  xs: "0.25rem"
  sm: "0.5rem"
  md: "0.75rem"
  lg: "1rem"
  xl: "1.5rem"
  xxl: "2rem"
  section: "3rem"
  page: "1.25rem"
radii:
  none: "0"
  small: "0.25rem"
  medium: "0.5rem"
  large: "0.75rem"
  full: "9999px"
shadows:
  none: "none"
  subtle: "0 1px 2px rgba(0, 0, 0, 0.35)"
  panel: "0 4px 20px rgba(0, 0, 0, 0.45)"
  popover: "0 10px 35px rgba(0, 0, 0, 0.5)"
  focus_ring: "0 0 0 2px rgba(96, 165, 250, 0.35)"
breakpoints:
  mobile: "36rem"
  tablet: "48rem"
  desktop: "64rem"
  wide: "90rem"
---

# Design Contract: Zinc Operational Console

This file defines the default visual style for generated web scaffolds.

- DESIGN.md is a visual contract for AI agents.
- DESIGN.md is not a source for WHAT or WHY requirements.

## Visual Theme

- The default theme is **Zinc Operational Console**.
- Use a dark, restrained zinc base for surface hierarchy.
- Apply muted contrast in non-critical text and high contrast for critical text.
- Keep interaction states clear using semantic emphasis colors.
- Favor dense, operational spacing and sharp-but-consistent radii.

## Colors And Semantic Roles

### Zinc foundations

- `colors.zinc.surfaces` defines page, panel, card, and sidebar surfaces.
- `colors.zinc.text` defines high / normal / muted / disabled text roles.
- `colors.zinc.borders` defines border hierarchy and focus emphasis.
- `colors.zinc.focus` defines focus ring and glow treatment.
- Use the zinc baseline before applying semantic roles.

### Semantic roles

- `colors.zinc.semantic.primary`: restrained blue action and emphasis.
- `colors.zinc.semantic.success`: emerald for positive/ok states.
- `colors.zinc.semantic.warning`: amber for caution states.
- `colors.zinc.semantic.danger`: red for destructive/error states.
- `colors.zinc.semantic.info`: cyan for informational badges and helper tone.
- `colors.zinc.semantic.muted`: soft muted tone for low-emphasis surfaces and separators.

## Typography

- Use `typography.font_family.sans` for interface copy and `typography.font_family.mono` for fixed-width content.
- Use `typography.scale` for size hierarchy.
- Use `typography.line_height` values to keep dense layouts readable.
- Use `typography.weight` to differentiate hierarchy without introducing extra chrome.
- Keep `typography.tracking` within the defined tokens.

## Components

- Components should use semantic color tokens, spacing tokens, and radius/shadow tokens.
- Avoid inventing one-off design decisions not derivable from this contract.
- Prefer reusable classes and minimal visual noise.
- If a UI element is data-dense, prefer subdued borders and clear sectioning.

## Layout And Spacing

- Use tokenized spacing from `spacing.compact` through `spacing.page`.
- Page-level rhythm should start with `spacing.page` margins.
- Prefer section groupings and `spacing.section` gaps for scannable flows.

## Depth And Elevation

- Use `shadows.none` and `shadows.subtle` for base surfaces.
- Use `shadows.panel` for raised cards and `shadows.popover` for overlay surfaces.
- Use `shadows.focus_ring` only for focused or focused-hover states.

## Responsive Behavior

- Use `breakpoints.mobile`, `tablet`, `desktop`, and `wide` as the only canonical width boundaries.
- Preserve clarity at each breakpoint through density tuning, not brand expansion.
- Keep typography scale and spacing consistent across breakpoints unless constrained by viewport.

## Do/Don't

- Do use the zinc tokens to describe concrete visual values.
- Do keep semantic contrast high for status and focus.
- Do not define product features, workflows, architecture, or user value in this file.
- Do not use this file as a WHAT or WHY requirement source.
- Do not derive new use cases or acceptance criteria from `DESIGN.md`.
- Agents must not derive new use cases from `DESIGN.md`.
- Do not treat this file as runtime behavior, implementation logic, or process documentation.

## Agent Prompt Anchors

- Treat this file as the authoritative source for design tokens only.
- When asked for visual treatment in this repository, map decisions to the token names above.
- Confirm output preserves the `Zinc Operational Console` defaults before proposing styling changes.