---
name: Aether & Gold
colors:
  surface: '#16130f'
  surface-dim: '#16130f'
  surface-bright: '#3d3834'
  surface-container-lowest: '#110e0a'
  surface-container-low: '#1e1b17'
  surface-container: '#221f1b'
  surface-container-high: '#2d2925'
  surface-container-highest: '#38342f'
  on-surface: '#e9e1da'
  on-surface-variant: '#d1c5b6'
  inverse-surface: '#e9e1da'
  inverse-on-surface: '#34302b'
  outline: '#9a8f81'
  outline-variant: '#4e453a'
  surface-tint: '#e7c186'
  primary: '#e7c186'
  on-primary: '#432c00'
  primary-container: '#c6a26a'
  on-primary-container: '#513809'
  inverse-primary: '#765929'
  secondary: '#e2c19b'
  on-secondary: '#402d11'
  secondary-container: '#5c4528'
  on-secondary-container: '#d3b38e'
  tertiary: '#b1c8ee'
  on-tertiary: '#1a3150'
  tertiary-container: '#93a9ce'
  on-tertiary-container: '#283e5d'
  error: '#ffb4ab'
  on-error: '#690005'
  error-container: '#93000a'
  on-error-container: '#ffdad6'
  primary-fixed: '#ffdead'
  primary-fixed-dim: '#e7c186'
  on-primary-fixed: '#281900'
  on-primary-fixed-variant: '#5c4213'
  secondary-fixed: '#ffddb6'
  secondary-fixed-dim: '#e2c19b'
  on-secondary-fixed: '#291802'
  on-secondary-fixed-variant: '#594326'
  tertiary-fixed: '#d5e3ff'
  tertiary-fixed-dim: '#b1c8ee'
  on-tertiary-fixed: '#011c3a'
  on-tertiary-fixed-variant: '#324868'
  background: '#16130f'
  on-background: '#e9e1da'
  surface-variant: '#38342f'
typography:
  display-lg:
    fontFamily: EB Garamond
    fontSize: 72px
    fontWeight: '500'
    lineHeight: '1.1'
    letterSpacing: -0.02em
  headline-xl:
    fontFamily: EB Garamond
    fontSize: 48px
    fontWeight: '400'
    lineHeight: '1.2'
    letterSpacing: 0em
  headline-lg:
    fontFamily: EB Garamond
    fontSize: 32px
    fontWeight: '400'
    lineHeight: '1.3'
    letterSpacing: 0.02em
  body-lg:
    fontFamily: Manrope
    fontSize: 18px
    fontWeight: '400'
    lineHeight: '1.8'
    letterSpacing: 0.03em
  body-md:
    fontFamily: Manrope
    fontSize: 16px
    fontWeight: '400'
    lineHeight: '1.7'
    letterSpacing: 0.03em
  label-caps:
    fontFamily: Manrope
    fontSize: 12px
    fontWeight: '600'
    lineHeight: '1.5'
    letterSpacing: 0.15em
rounded:
  sm: 0.125rem
  DEFAULT: 0.25rem
  md: 0.375rem
  lg: 0.5rem
  xl: 0.75rem
  full: 9999px
spacing:
  grid-margin: 4rem
  grid-gutter: 2rem
  section-gap: 8rem
  stack-sm: 0.75rem
  stack-md: 1.5rem
  stack-lg: 3rem
---

## Brand & Style

This design system is built on a narrative of cinematic fantasy and editorial luxury. It targets a high-end audience that values craftsmanship, storytelling, and atmosphere. The visual language blends the raw mood of a dark fantasy film with the structured elegance of a premium fashion magazine.

The style is defined as **Editorial Noir**, characterized by:
- **Cinematic Depth:** High-contrast lighting and deep shadows to create a sense of mystery and importance.
- **Crafted Precision:** Use of metallic accents and fine lines to suggest hand-crafted quality.
- **Vastness:** Expansive use of whitespace (blackspace) to give content room to breathe and command attention.
- **Sophistication:** A rejection of generic UI trends in favor of timeless, serif-driven typography and tactile-inspired surfaces.

## Colors

The palette is rooted in a "Gilded Shadow" concept. The primary background is nearly black to create a void where imagery and light can pop. 

- **Primary Accent (Antique Gold):** Used for primary calls to action, active states, and critical decorative elements.
- **Secondary Accent (Soft Bronze):** Used for hover states and subtle hierarchy in interactive elements.
- **Neutral Surfaces:** The transition from `#0F0F10` to `#171514` defines content blocks without requiring heavy borders.
- **Typography:** Warm whites and beiges are used instead of pure white to maintain the "aged parchment" or "candlelit" feel of the cinematic theme.

## Typography

The typography system relies on a sharp contrast between the historical, elegant **EB Garamond** (representing the fantasy/narrative element) and the hyper-modern **Manrope** (representing the professional, functional interface).

- **Headings:** Should always use EB Garamond. For large display titles, use a tighter tracking. For sub-headers, allow more air.
- **Body:** Manrope is set with generous line heights (1.7+) and wide tracking (0.03em+) to ensure the dark theme remains highly readable and feels "luxury-editorial."
- **Labels:** Small caps with high tracking are used for categorizations (e.g., overlines) to provide a structural, navigational feel.

## Layout & Spacing

The layout follows a **Fluid 12-Column Grid** with extreme vertical rhythm to emphasize the cinematic pacing. 

- **Breathing Room:** Content sections are separated by large gaps (`8rem` or more) to prevent the dark interface from feeling claustrophobic.
- **Alignment:** While the grid is fluid, content should often be center-aligned or offset in a "broken grid" fashion to mimic high-end magazine layouts.
- **Mobile Reflow:** On mobile, margins reduce to `1.5rem`, and the 12-column grid collapses to 1 column, while maintaining the vertical section gaps to preserve the editorial feel.

## Elevation & Depth

In this system, depth is conveyed through **Light Contrast** and **Atmospheric Blurring** rather than traditional shadows.

- **Tonal Layering:** Interactive surfaces (like card backgrounds) use the Secondary Background (`#171514`) against the Primary Background (`#0F0F10`).
- **Low-Contrast Outlines:** Borders should be treated as "threads of gold." Use the Antique Gold color at 15-20% opacity for borders.
- **Glow Effects:** Instead of drop shadows, use a very faint, large-radius outer glow of the Accent Gold (5% opacity) to give the impression that the element is backlit by a distant candle or light source.
- **Backdrop Blurs:** Navigation bars and overlays use a high-density background blur (20px+) with a semi-transparent dark tint.

## Shapes

The shape language is primarily **Rectilinear and Sharp**. Curves are kept to an absolute minimum to maintain a sense of formal architecture and structure.

- **Standard Elements:** Use a subtle `0.25rem` radius (Soft) to keep edges from appearing digitally harsh while maintaining a "cut" look.
- **Interactive States:** Buttons and Inputs should remain strictly rectangular or use the minimal `0.25rem` radius. 
- **Imagery:** Media should always have sharp corners (`0px`) to feel like framed canvases or cinematic stills.

## Components

### Buttons
- **Primary:** Solid Antique Gold fill with Deep Charcoal text. No border. Strict rectangular shape.
- **Secondary:** Transparent fill with a 1px Gold border at 40% opacity. Text in Gold.
- **Interaction:** On hover, the primary button shifts to the Bronze accent.

### Cards
- **Structure:** Background in `#171514`. 1px border in Gold at 20% opacity. 
- **Padding:** Generous internal padding (`3rem`) to emphasize luxury.
- **Imagery:** Full-bleed at the top of the card with a slight gradient overlay at the bottom to transition into text.

### Input Fields
- **Style:** Underline-only or 1px border. Dark background.
- **Focus:** Border opacity increases to 100% Gold. Text label floats above in small-caps Manrope.

### Lists & Navigation
- **Nav Links:** Manrope in label-caps. Subtle gold dot or underline appears on hover/active states.
- **List Items:** Separated by thin, low-opacity gold horizontal rules.

### Icons
- **Style:** 1.5pt stroke weight. Minimalist geometric style. Always rendered in Antique Gold.