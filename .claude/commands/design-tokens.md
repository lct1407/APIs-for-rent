---
description: Review and update design system tokens (colors, spacing, typography)
---

Review the current design system and suggest improvements or generate new design tokens.

## Design Token Categories

### 1. Color Tokens

Review and update the color system:

```bash
# Check current colors
cat client/src/index.css
cat client/tailwind.config.js
```

**Generate enhanced color palette**:

```css
:root {
  /* Primary Brand Colors */
  --brand-50: 250 245 255;
  --brand-100: 243 232 255;
  --brand-200: 233 213 255;
  --brand-300: 216 180 254;
  --brand-400: 192 132 252;
  --brand-500: 168 85 247;   /* Primary */
  --brand-600: 147 51 234;
  --brand-700: 126 34 206;
  --brand-800: 107 33 168;
  --brand-900: 88 28 135;
  --brand-950: 59 7 100;

  /* Semantic Colors */
  --success-50: 240 253 244;
  --success-500: 34 197 94;
  --success-900: 20 83 45;

  --warning-50: 255 251 235;
  --warning-500: 234 179 8;
  --warning-900: 113 63 18;

  --error-50: 254 242 242;
  --error-500: 239 68 68;
  --error-900: 127 29 29;

  --info-50: 239 246 255;
  --info-500: 59 130 246;
  --info-900: 30 58 138;
}
```

**Color Usage Guidelines**:
- 50-100: Backgrounds, subtle accents
- 200-400: Borders, disabled states
- 500-600: Primary actions, text
- 700-900: Hover states, active states
- 950: Deep shadows, very dark text

### 2. Spacing Tokens

Create consistent spacing scale:

```css
:root {
  /* Spacing Scale (based on 4px) */
  --space-0: 0;
  --space-px: 1px;
  --space-0-5: 0.125rem;  /* 2px */
  --space-1: 0.25rem;     /* 4px */
  --space-1-5: 0.375rem;  /* 6px */
  --space-2: 0.5rem;      /* 8px */
  --space-2-5: 0.625rem;  /* 10px */
  --space-3: 0.75rem;     /* 12px */
  --space-3-5: 0.875rem;  /* 14px */
  --space-4: 1rem;        /* 16px */
  --space-5: 1.25rem;     /* 20px */
  --space-6: 1.5rem;      /* 24px */
  --space-7: 1.75rem;     /* 28px */
  --space-8: 2rem;        /* 32px */
  --space-9: 2.25rem;     /* 36px */
  --space-10: 2.5rem;     /* 40px */
  --space-11: 2.75rem;    /* 44px */
  --space-12: 3rem;       /* 48px */
  --space-14: 3.5rem;     /* 56px */
  --space-16: 4rem;       /* 64px */
  --space-20: 5rem;       /* 80px */
  --space-24: 6rem;       /* 96px */
  --space-28: 7rem;       /* 112px */
  --space-32: 8rem;       /* 128px */
}
```

### 3. Typography Tokens

Create type scale:

```css
:root {
  /* Font Families */
  --font-sans: ui-sans-serif, system-ui, -apple-system, sans-serif;
  --font-serif: ui-serif, Georgia, Cambria, serif;
  --font-mono: ui-monospace, 'Cascadia Code', 'Fira Code', monospace;

  /* Font Sizes */
  --text-xs: 0.75rem;      /* 12px */
  --text-sm: 0.875rem;     /* 14px */
  --text-base: 1rem;       /* 16px */
  --text-lg: 1.125rem;     /* 18px */
  --text-xl: 1.25rem;      /* 20px */
  --text-2xl: 1.5rem;      /* 24px */
  --text-3xl: 1.875rem;    /* 30px */
  --text-4xl: 2.25rem;     /* 36px */
  --text-5xl: 3rem;        /* 48px */
  --text-6xl: 3.75rem;     /* 60px */
  --text-7xl: 4.5rem;      /* 72px */
  --text-8xl: 6rem;        /* 96px */
  --text-9xl: 8rem;        /* 128px */

  /* Font Weights */
  --font-thin: 100;
  --font-extralight: 200;
  --font-light: 300;
  --font-normal: 400;
  --font-medium: 500;
  --font-semibold: 600;
  --font-bold: 700;
  --font-extrabold: 800;
  --font-black: 900;

  /* Line Heights */
  --leading-none: 1;
  --leading-tight: 1.25;
  --leading-snug: 1.375;
  --leading-normal: 1.5;
  --leading-relaxed: 1.625;
  --leading-loose: 2;

  /* Letter Spacing */
  --tracking-tighter: -0.05em;
  --tracking-tight: -0.025em;
  --tracking-normal: 0em;
  --tracking-wide: 0.025em;
  --tracking-wider: 0.05em;
  --tracking-widest: 0.1em;
}
```

### 4. Border Radius Tokens

```css
:root {
  --radius-none: 0;
  --radius-sm: 0.125rem;   /* 2px */
  --radius-base: 0.25rem;  /* 4px */
  --radius-md: 0.375rem;   /* 6px */
  --radius-lg: 0.5rem;     /* 8px */
  --radius-xl: 0.75rem;    /* 12px */
  --radius-2xl: 1rem;      /* 16px */
  --radius-3xl: 1.5rem;    /* 24px */
  --radius-full: 9999px;
}
```

### 5. Shadow Tokens

```css
:root {
  /* Elevation Shadows */
  --shadow-xs: 0 1px 2px 0 rgb(0 0 0 / 0.05);
  --shadow-sm: 0 1px 3px 0 rgb(0 0 0 / 0.1), 0 1px 2px -1px rgb(0 0 0 / 0.1);
  --shadow-md: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);
  --shadow-lg: 0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1);
  --shadow-xl: 0 20px 25px -5px rgb(0 0 0 / 0.1), 0 8px 10px -6px rgb(0 0 0 / 0.1);
  --shadow-2xl: 0 25px 50px -12px rgb(0 0 0 / 0.25);
  --shadow-inner: inset 0 2px 4px 0 rgb(0 0 0 / 0.05);

  /* Colored Shadows */
  --shadow-primary: 0 10px 15px -3px rgb(168 85 247 / 0.3);
  --shadow-success: 0 10px 15px -3px rgb(34 197 94 / 0.3);
  --shadow-error: 0 10px 15px -3px rgb(239 68 68 / 0.3);
}
```

### 6. Animation Tokens

```css
:root {
  /* Duration */
  --duration-75: 75ms;
  --duration-100: 100ms;
  --duration-150: 150ms;
  --duration-200: 200ms;
  --duration-300: 300ms;
  --duration-500: 500ms;
  --duration-700: 700ms;
  --duration-1000: 1000ms;

  /* Easing */
  --ease-linear: linear;
  --ease-in: cubic-bezier(0.4, 0, 1, 1);
  --ease-out: cubic-bezier(0, 0, 0.2, 1);
  --ease-in-out: cubic-bezier(0.4, 0, 0.2, 1);
  --ease-bounce: cubic-bezier(0.68, -0.55, 0.265, 1.55);
  --ease-elastic: cubic-bezier(0.68, -0.6, 0.32, 1.6);
}
```

### 7. Z-Index Tokens

```css
:root {
  --z-0: 0;
  --z-10: 10;
  --z-20: 20;
  --z-30: 30;
  --z-40: 40;
  --z-50: 50;
  --z-auto: auto;

  /* Named layers */
  --z-dropdown: 1000;
  --z-sticky: 1020;
  --z-fixed: 1030;
  --z-modal-backdrop: 1040;
  --z-modal: 1050;
  --z-popover: 1060;
  --z-tooltip: 1070;
  --z-notification: 1080;
}
```

## Review Checklist

When reviewing design tokens:

- [ ] **Consistency**: Are tokens used consistently across components?
- [ ] **Completeness**: Do we have tokens for all use cases?
- [ ] **Naming**: Are token names clear and semantic?
- [ ] **Documentation**: Are tokens documented with usage guidelines?
- [ ] **Accessibility**: Do color combinations meet WCAG standards?
- [ ] **Dark Mode**: Do tokens work in both light and dark modes?
- [ ] **Scale**: Do spacing/typography scales feel harmonious?
- [ ] **Performance**: Are we using CSS custom properties efficiently?

## Generate Token Documentation

Create a visual token reference:

```tsx
// DesignTokens.tsx - Visual reference page
export function DesignTokens() {
  return (
    <div className="p-8 space-y-12">
      {/* Colors */}
      <section>
        <h2 className="text-3xl font-bold mb-6">Colors</h2>
        <div className="grid grid-cols-10 gap-2">
          {[50, 100, 200, 300, 400, 500, 600, 700, 800, 900].map(shade => (
            <div key={shade}>
              <div className={`h-20 rounded-lg bg-brand-${shade}`}></div>
              <p className="text-sm mt-2">{shade}</p>
            </div>
          ))}
        </div>
      </section>

      {/* Typography */}
      <section>
        <h2 className="text-3xl font-bold mb-6">Typography</h2>
        <div className="space-y-4">
          <p className="text-xs">Extra Small (12px)</p>
          <p className="text-sm">Small (14px)</p>
          <p className="text-base">Base (16px)</p>
          <p className="text-lg">Large (18px)</p>
          <p className="text-xl">Extra Large (20px)</p>
          <p className="text-2xl">2XL (24px)</p>
        </div>
      </section>

      {/* Spacing */}
      <section>
        <h2 className="text-3xl font-bold mb-6">Spacing</h2>
        {/* Visual spacing scale */}
      </section>
    </div>
  )
}
```

## Output

Provide:
1. **Current Token Analysis**: What tokens exist and how they're used
2. **Recommendations**: Suggested improvements
3. **New Tokens**: Any missing tokens to add
4. **Usage Examples**: How to use tokens in components
5. **Migration Guide**: If changing existing tokens
6. **Visual Reference**: Component to visualize tokens
