# iCL Design Tokens — Full CSS Custom Properties

Use this as a starter template when scaffolding a new project or component.

```css
:root {
  /* ========== COLORS ========== */

  /* Gray / Neutral */
  --color-white: #FFFFFF;
  --color-black: #101010;
  --color-neutral-900: #212529;
  --color-neutral-400: #CED4DA;
  --color-gray-500: #F7F8F7;
  --color-gray-700: #F0F0F0;
  --color-gray-1000: #CCCCCC;

  /* Green (Primary / Brand) */
  --color-green-primary: #458500;
  --color-green-100: #E5F8E6;
  --color-green-200: #C8E6C9;
  --color-green-400: #2C7500;
  --color-green-500: #386B00;

  /* Orange (Secondary) */
  --color-orange-secondary: #F38A00;
  --color-orange-100: #FFF3E2;
  --color-orange-200: #F5DDBA;
  --color-orange-400: #AF3500;
  --color-orange-500: #8F2B00;

  /* Blue (Info / Links) */
  --color-blue-100: #E2F2FF;
  --color-blue-200: #BBDEFB;
  --color-blue-400: #126CC5;
  --color-blue-500: #004E9B;

  /* Yellow (Warning) */
  --color-yellow-100: #FEFAD8;
  --color-yellow-200: #F6EB8A;
  --color-yellow-300: #FAC627;
  --color-yellow-400: #8A6702;
  --color-yellow-500: #5E4500;

  /* Red (Error / Action) */
  --color-red-100: #FFECEC;
  --color-red-200: #F4CFCF;
  --color-red-400: #CA2222;
  --color-red-500: #AD0601;

  /* ========== SEMANTIC TEXT ========== */
  --color-text-primary: #333333;
  --color-text-secondary: #666666;
  --color-text-link: #126CC5;
  --color-text-emphasis: #2C7500;
  --color-text-promo: #F38A00;
  --color-text-error: #CA2222;
  --color-text-white: #FFFFFF;
  --color-text-disabled: #9F9F9F;

  /* ========== BACKGROUNDS & BORDERS ========== */
  --color-bg-white: #FFFFFF;
  --color-bg-gray: #F7F8F7;
  --color-bg-black: #101010;
  --color-border: #CCCCCC;
  --color-divider: #E0E0E0;
  --color-skeleton: #F5F5F5;

  /* ========== SPACING ========== */
  --spacing-xxxs: 2px;
  --spacing-xxs: 4px;
  --spacing-xs: 8px;
  --spacing-sm: 12px;
  --spacing-md: 16px;
  --spacing-lg: 20px;
  --spacing-xl: 24px;
  --spacing-xxl: 32px;

  /* ========== BORDER RADIUS ========== */
  --radius-none: 0;
  --radius-xs: 4px;
  --radius-sm: 6px;
  --radius-md: 8px;
  --radius-lg: 12px;
  --radius-xl: 16px;
  --radius-full: 9999px;

  /* ========== ELEVATION / SHADOWS ========== */
  --elevation-1: 0px 2px 8px rgba(0, 0, 0, 0.12);
  --elevation-2: 0px 3px 8px rgba(0, 0, 0, 0.06), 0px 6px 8px rgba(0, 0, 0, 0.12);
  --elevation-3: 0px 12px 20px rgba(0, 0, 0, 0.16);
  --elevation-top: 0px -2px 8px rgba(0, 0, 0, 0.12);
  --elevation-left: -4px 2px 10px rgba(0, 0, 0, 0.12);
  --elevation-right: 4px 0px 10px rgba(0, 0, 0, 0.12);
  --elevation-bottom: 0px 4px 10px rgba(0, 0, 0, 0.12);

  /* ========== BREAKPOINTS (reference only — use in @media) ========== */
  /* xs: 375px  | sm: 490px  | md: 768px */
  /* lg: 1080px | xl: 1440px | xxl: 1920px */

  /* ========== TYPOGRAPHY ========== */
  --font-family: 'Noto Sans', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  --font-weight-regular: 400;
  --font-weight-bold: 700;

  --font-size-tiny: 0.75rem;    /* 12px */
  --font-size-small: 0.875rem;  /* 14px */
  --font-size-body: 1rem;       /* 16px */
  --font-size-subtitle: 1.125rem; /* 18px */
  --font-size-section: 1.25rem; /* 20px */
  --font-size-page: 1.5rem;     /* 24px */
  --font-size-h2: 1.75rem;      /* 28px */
  --font-size-h1: 2rem;         /* 32px */

  --line-height-tiny: 1rem;     /* 16px */
  --line-height-small: 1.25rem; /* 20px */
  --line-height-body: 1.5rem;   /* 24px */
  --line-height-section: 1.625rem; /* 26px */
  --line-height-page: 1.875rem; /* 30px */
  --line-height-h2: 2.25rem;    /* 36px */
  --line-height-h1: 2.5rem;     /* 40px */
}
```

## Responsive Typography Mixin Pattern

```css
/* Mobile-first: start with mobile sizes, scale up at md breakpoint */
h1 { font-size: 1.75rem; line-height: 2.25rem; font-weight: 700; }
h2 { font-size: 1.5rem;  line-height: 1.875rem; font-weight: 700; }
h3 { font-size: 1.25rem; line-height: 1.625rem; font-weight: 700; }
h4 { font-size: 1.125rem; line-height: 1.5rem; font-weight: 700; }
h5 { font-size: 1rem;    line-height: 1.5rem; font-weight: 700; }
h6 { font-size: 1rem;    line-height: 1.5rem; font-weight: 700; }

@media (min-width: 768px) {
  h1 { font-size: 2rem;     line-height: 2.5rem; }
  h2 { font-size: 1.75rem;  line-height: 2.25rem; }
  h3 { font-size: 1.5rem;   line-height: 1.875rem; }
  h4 { font-size: 1.25rem;  line-height: 1.625rem; }
  h5 { font-size: 1.125rem; line-height: 1.5rem; }
  h6 { font-size: 0.875rem; line-height: 1.25rem; }
}
```

## Media Query Helpers

```css
/* Mobile-first breakpoints */
@media (min-width: 375px)  { /* xs — small mobile */ }
@media (min-width: 490px)  { /* sm — large mobile */ }
@media (min-width: 768px)  { /* md — tablet, switch to desktop typography */ }
@media (min-width: 1080px) { /* lg — small desktop */ }
@media (min-width: 1440px) { /* xl — desktop */ }
@media (min-width: 1920px) { /* xxl — large desktop, center in 1440px container */ }
```
