# Advanced v4 Patterns, Migration & Best Practices

## Table of Contents
1. [Custom Utilities](#custom-utilities)
2. [Theme Modifiers](#theme-modifiers)
3. [Namespace Overrides](#namespace-overrides)
4. [Semi-transparent Color Variants](#semi-transparent-color-variants)
5. [Container Queries](#container-queries)
6. [v3 to v4 Migration Checklist](#v3-to-v4-migration-checklist)
7. [Best Practices](#best-practices)
8. [Resources](#resources)

---

## Custom Utilities

Define reusable custom utilities with `@utility`:

```css
/* Decorative full-width lines */
@utility line-t {
  @apply relative before:absolute before:top-0 before:-left-[100vw] before:h-px before:w-[200vw] before:bg-gray-950/5 dark:before:bg-white/10;
}

/* Text gradient */
@utility text-gradient {
  @apply bg-gradient-to-r from-primary to-accent bg-clip-text text-transparent;
}
```

---

## Theme Modifiers

```css
/* @theme inline — references other CSS variables (resolved at use-time) */
@theme inline {
  --font-sans: var(--font-inter), system-ui;
}

/* @theme static — always generate CSS variables even when unused */
@theme static {
  --color-brand: oklch(65% 0.15 240);
}

/* Import with static theme */
@import "tailwindcss" theme(static);
```

---

## Namespace Overrides

```css
@theme {
  /* Clear all default colors and define your own */
  --color-*: initial;
  --color-white: #fff;
  --color-black: #000;
  --color-primary: oklch(45% 0.2 260);
  --color-secondary: oklch(65% 0.15 200);

  /* Clear ALL defaults for a minimal setup */
  /* --*: initial; */
}
```

---

## Semi-transparent Color Variants

```css
@theme {
  /* Use color-mix() for alpha variants */
  --color-primary-50:  color-mix(in oklab, var(--color-primary)  5%, transparent);
  --color-primary-100: color-mix(in oklab, var(--color-primary) 10%, transparent);
  --color-primary-200: color-mix(in oklab, var(--color-primary) 20%, transparent);
}
```

---

## Container Queries

```css
@theme {
  --container-xs: 20rem;
  --container-sm: 24rem;
  --container-md: 28rem;
  --container-lg: 32rem;
}
```

---

## v3 to v4 Migration Checklist

- [ ] Replace `tailwind.config.ts` with CSS `@theme` block
- [ ] Change `@tailwind base/components/utilities` → `@import "tailwindcss"`
- [ ] Move color definitions to `@theme { --color-*: value }`
- [ ] Replace `darkMode: "class"` with `@custom-variant dark (&:where(.dark, .dark *))`
- [ ] Move `@keyframes` inside `@theme` blocks (ensures keyframes output with theme)
- [ ] Replace `require("tailwindcss-animate")` with native CSS animations
- [ ] Update `h-10 w-10` → `size-10` (new utility)
- [ ] Remove `forwardRef` (React 19 passes ref as prop)
- [ ] Consider OKLCH colors for better color perception
- [ ] Replace custom plugins with `@utility` directives

---

## Best Practices

**Do:**
- Use `@theme` blocks — CSS-first configuration is v4's core pattern
- Use OKLCH colors — better perceptual uniformity than HSL
- Compose components with CVA — type-safe variants
- Use semantic tokens — `bg-primary` not `bg-blue-500`
- Use `size-*` — new shorthand for `w-* h-*`
- Add ARIA attributes and visible focus states for accessibility

**Don't:**
- Use `tailwind.config.ts` — use CSS `@theme` instead
- Use `@tailwind` directives — use `@import "tailwindcss"`
- Use `forwardRef` — React 19 passes ref as prop
- Use arbitrary values — extend `@theme` instead
- Hardcode colors — use semantic tokens
- Skip dark mode testing — test both themes

---

## Resources

- [Tailwind CSS v4 Documentation](https://tailwindcss.com/docs)
- [Tailwind v4 Beta Announcement](https://tailwindcss.com/blog/tailwindcss-v4-beta)
- [CVA Documentation](https://cva.style/docs)
- [shadcn/ui](https://ui.shadcn.com/)
- [Radix Primitives](https://www.radix-ui.com/primitives)
