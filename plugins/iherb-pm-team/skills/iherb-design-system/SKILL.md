---
name: iherb-design-system
description: iHerb Design System (iCL — iHerb Component Library). Use when building UI that follows iHerb's brand and design standards. Covers colors, typography, spacing, layout, components, and interaction patterns extracted from the official Figma component library.
---

# iHerb Design System (iCL)

Apply these tokens, patterns, and component specs when building UI for iHerb or projects that follow iHerb design standards.

- **`references/tokens.md`** — Full CSS custom properties template. Copy into new projects as a starting point.
- **`references/components.md`** — Complete inventory of 80+ components from the Figma library. Check before building custom UI.

## Design Principles

- **Mobile-first.** Design for 375px, then scale up. Typography and layout adapt at the `md` (768px) breakpoint.
- **Token-driven.** Use design tokens for all colors, spacing, radii, and shadows. Never use arbitrary values.
- **Accessible.** Target WCAG AA contrast. All interactive elements need visible focus states and 48px minimum touch targets on mobile.

---

## Brand Colors

| Role | Token | Hex | Usage |
|---|---|---|---|
| Primary | `--color-green-primary` | `#458500` | Brand CTA, header bg, active states |
| Secondary | `--color-orange-secondary` | `#F38A00` | Promo text, sale badges |
| Info / Link | `--color-blue-400` | `#126CC5` | Hyperlinks, focus rings |
| Error | `--color-red-400` | `#CA2222` | Error messages, discount prices |
| Emphasis | `--color-green-400` | `#2C7500` | Trial pricing, important highlights |

### Color Scale

Each hue has a 100–500 scale: 100 = light background tint, 200 = light border/accent, 400 = emphasis/dark, 500 = darkest.

| Hue | 100 | 200 | 400 | 500 |
|---|---|---|---|---|
| Green | `#E5F8E6` | `#C8E6C9` | `#2C7500` | `#386B00` |
| Orange | `#FFF3E2` | `#F5DDBA` | `#AF3500` | `#8F2B00` |
| Blue | `#E2F2FF` | `#BBDEFB` | `#126CC5` | `#004E9B` |
| Yellow | `#FEFAD8` | `#F6EB8A` | `#8A6702` | `#5E4500` |
| Red | `#FFECEC` | `#F4CFCF` | `#CA2222` | `#AD0601` |

### Neutrals

| Token | Hex | Usage |
|---|---|---|
| White | `#FFFFFF` | Page background |
| Black | `#101010` | Darkest text, dark-theme bg |
| Text primary | `#333333` | Default body text |
| Text secondary | `#666666` | Supporting text |
| Text disabled | `#9F9F9F` | Disabled controls |
| BG gray | `#F7F8F7` | Section backgrounds |
| BG gray dark | `#F0F0F0` | Darker section fills |
| Border | `#CCCCCC` | Card borders, input borders |
| Divider | `#E0E0E0` | Horizontal rules, separators |
| Skeleton | `#F5F5F5` | Loading placeholder bg |

---

## Typography

**Font:** Noto Sans (variable). **Base:** 1rem = 16px. **Weights:** 400 (regular), 700 (bold).

### Heading Scale (mobile / desktop)

| Level | Mobile | Desktop | Weight |
|---|---|---|---|
| H1 | 28/36 | 32/40 | 700 |
| H2 | 24/30 | 28/36 | 700 |
| H3 | 20/26 | 24/30 | 700 |
| H4 | 18/24 | 20/26 | 700 |
| H5 | 16/24 | 18/24 | 700 |
| H6 | 16/24 | 14/20 | 700 |

### Body Scale

| Style | Size/LH | Weight |
|---|---|---|
| Body | 16/24 | 400 |
| Small | 14/20 | 400 |
| Tiny | 12/16 | 400 |

### Article Styles

For long-form content, use article variants with 140–180% line heights. Article sizes mirror headings but with more generous line spacing for readability. See `references/tokens.md` for full article scale.

Switch from mobile to desktop typography at **768px** (`--breakpoint-md`).

---

## Spacing

8px base grid with small additions at the edges of the scale.

| Token | Value |
|---|---|
| `xxxs` | 2px |
| `xxs` | 4px |
| `xs` | 8px |
| `sm` | 12px |
| `md` | 16px |
| `lg` | 20px |
| `xl` | 24px |
| `xxl` | 32px |

Use these for padding, margin, and gap. Pick from the scale — don't invent values.

---

## Border Radius

| Token | Value | When to use |
|---|---|---|
| `none` | 0 | Sharp edges (tables, full-bleed) |
| `xs` | 4px | Tags, small chips |
| `sm` | 6px | Small buttons, inputs |
| `md` | 8px | Cards, large buttons |
| `lg` | 12px | Modals, panels |
| `xl` | 16px | Large containers |
| `full` | 9999px | Pills, avatars, search bar |

---

## Elevation

| Level | Shadow | When to use |
|---|---|---|
| 1 | `0 2px 8px rgba(0,0,0,0.12)` | Cards, dropdowns |
| 2 | `0 3px 8px rgba(0,0,0,0.06), 0 6px 8px rgba(0,0,0,0.12)` | Popovers, floating panels |
| 3 | `0 12px 20px rgba(0,0,0,0.16)` | Modals, dialogs |
| Directional | top / left / right / bottom variants | Sticky headers, side panels |

---

## Layout & Breakpoints

| Breakpoint | Width | Padding | Main Area |
|---|---|---|---|
| xs (mobile) | 393px | 16px | 361px |
| md (tablet) | 768px | 24px | 720px |
| lg (sm desktop) | 1080px | 32px | 1016px |
| xl (desktop) | 1440px | 32px | 1376px |
| xxl (lg desktop) | 1920px | 32px | 1376px (in 1440px centered container) |

At **1920px+**, wrap content in a 1440px max-width centered container. Carousels and hero sections can extend full-bleed to body width.

---

## Components

### Filled Button (Primary CTA)

| Property | Large | Small |
|---|---|---|
| Font size (desktop) | 16px bold | 14px bold |
| Border radius | 8px (`md`) | 6px (`sm`) |
| Min touch target (mobile) | 48px | 48px |

**States:**
- **Default:** Green bg `#458500`, white text
- **Hover:** Darken bg
- **Pressed:** Darken further
- **Focus:** 3px outer ring `#126CC5` + 1px inner white ring
- **Disabled:** `#9F9F9F` text, muted bg
- **Skeleton:** `#F5F5F5` bg placeholder

### Plain Button (Text Button)

Same sizing as Filled Button. No background (transparent).

**States:**
- **Default:** Blue text `#126CC5`
- **Hover/Pressed:** Add underline
- **Focus:** Same 3px blue + 1px white ring
- **Disabled:** `#9F9F9F` text
- Supports both light and dark theme variants

### Box

Container component with configurable:
- **Border radius:** Any value from radius scale
- **Background:** transparent, white, or gray (`#F7F8F7`)
- **Border:** Optional, uses `#CCCCCC`

### App Header

- Background: Primary green `#458500`
- White text and icons
- Search input with pill shape (`radius-full`)
- Placeholder: "Search iHerb"

### Navigation Tab Bar (Mobile Footer)

- 5 tabs: Home, Explore, Category, Cart, Me
- **Active:** Green pill bg `#E5F8E6`, green text `#2C7500`
- **Inactive:** Secondary text `#666666`
- Cart badge: Green circle `#458500` with white bold count
- Icon: 24px, Label: 12px regular
- Top border shadow (elevation-1) + divider border

---

## Focus & Interaction Patterns

All interactive elements share a consistent focus style:
- **Focus ring:** 3px outer border `#126CC5` + 1px inner white border
- **Touch targets:** Minimum 48px on mobile (enforced via padding or min-height)
- **Skeleton loading:** Replace content with `#F5F5F5` rounded rectangles matching component dimensions
- **Disabled:** Gray out with `#9F9F9F` text, reduce opacity where appropriate

---

## Implementation Checklist

When building a new view or component:

1. Copy CSS custom properties from `references/tokens.md` into your project
2. Set up Noto Sans via Google Fonts or local `@font-face`
3. Start with mobile layout (393px body, 16px padding, 361px main area)
4. Add responsive breakpoints at 768px (tablet) and 1080px+ (desktop)
5. At 1920px+, wrap in a 1440px max-width centered container
6. Apply spacing tokens to all padding, margin, and gap
7. Use radius tokens from the scale for all rounded corners
8. Implement all interactive states: default, hover, pressed, focus, disabled, skeleton
9. Verify WCAG AA contrast for all text-on-background combinations
10. Ensure 48px touch targets for all tappable elements on mobile
