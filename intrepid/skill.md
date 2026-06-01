---
name: phoenix-design-system
description: This skill should be used when the user asks to "use Phoenix tokens", "build a Phoenix component", "follow Phoenix design system", "add pnx- styles", "use the design system", "what component should I use", or any question about Intrepid's design system tokens, SCSS patterns, or component API. Provides Phoenix Design System guidance for Vue/Nuxt, mobile, email, and Salesforce teams.
---

# Phoenix Design System

Phoenix is Intrepid Group's design system powering web, mobile, email, and Salesforce surfaces. CSS prefix `pnx-`. BEM convention: `pnx-block__element--modifier`. Never hardcode design values — always use tokens.

---

## The 5 Non-Negotiable Rules

1. **Never hardcode colors, spacing, or font sizes.** Use CSS custom properties (`var(--pnx-*)`) for runtime-themeable values, or SCSS variables (`$spacing-m`, `$brand-primary-intrepid-red`) for build-time values.
2. **Use `@include breakpoint('md')` — never raw `@media` queries.** Import mixins before calling them.
3. **Component SCSS: use `@import` (legacy pattern) then unnamespaced mixin calls.** Do not use `@use` in component `.scss` files — the project uses the legacy `@import` pipeline.
4. **`<script setup lang="ts">` only.** No Options API, no class components.
5. **Apply theme on the root element via class.** Available themes: `pnx-theme--light`, `pnx-theme--dark`, `pnx-theme--high-contrast`, `pnx-theme--muir`.

---

## Key Token Quick Reference

### Brand Primary Colors

| Token        | SCSS Variable                 | CSS Custom Property                             | Hex       |
| ------------ | ----------------------------- | ----------------------------------------------- | --------- |
| intrepid-red | `$brand-primary-intrepid-red` | `var(--pnx-brand-palette-primary-intrepid-red)` | `#ff2828` |
| midnight     | `$brand-primary-midnight`     | `var(--pnx-brand-palette-primary-midnight)`     | `#222222` |
| sand         | `$brand-primary-sand`         | `var(--pnx-brand-palette-primary-sand)`         | `#f6f4f0` |
| wet-sand     | `$brand-primary-wet-sand`     | `var(--pnx-brand-palette-primary-wet-sand)`     | `#e6e1d7` |
| white        | `$brand-primary-white`        | `var(--pnx-brand-palette-primary-white)`        | `#ffffff` |

### UI Text Colors (Light Theme)

| Token         | CSS Custom Property                        | Value              |
| ------------- | ------------------------------------------ | ------------------ |
| text-primary  | `var(--pnx-ui-palette-text-text-primary)`  | `rgb(0 0 0 / 86%)` |
| text-weak     | `var(--pnx-ui-palette-text-text-weak)`     | `#757575`          |
| text-link     | `var(--pnx-ui-palette-text-text-link)`     | `#0042e5`          |
| text-disabled | `var(--pnx-ui-palette-text-text-disabled)` | `#bebebe`          |

### Spacing (Desktop)

| Key | SCSS Variable  | Value           |
| --- | -------------- | --------------- |
| xxs | `$spacing-xxs` | `0.5rem / 8px`  |
| xs  | `$spacing-xs`  | `1rem / 16px`   |
| s   | `$spacing-s`   | `1.5rem / 24px` |
| m   | `$spacing-m`   | `2rem / 32px`   |
| l   | `$spacing-l`   | `2.5rem / 40px` |
| xl  | `$spacing-xl`  | `5rem / 80px`   |
| xxl | `$spacing-xxl` | `10rem / 160px` |

Base unit: 8px. All spacing steps are multiples of 8.

### Shadows

| Token        | Value                              |
| ------------ | ---------------------------------- |
| shadow-1     | `0 2px 8px 0 rgb(0 0 0 / 14%)`     |
| shadow-2     | `0 4px 24px 0 rgb(0 0 0 / 14%)`    |
| shadow-3     | `0 8px 24px 3px rgb(0 0 0 / 14%)`  |
| shadow-4     | `0 16px 24px 4px rgb(0 0 0 / 14%)` |
| shadow-5     | `0 24px 48px 6px rgb(0 0 0 / 18%)` |
| shadow-focus | `0 0 16px 5px rgb(0 0 0 / 18%)`    |

Use `@include shadow(2)` — pass elevation number 1–5.

### Animation

| Token   | Value   |
| ------- | ------- |
| fast    | `0.15s` |
| default | `0.3s`  |
| slow    | `0.5s`  |

---

## Component Groups

### Forms & Inputs

`PhoenixTextField`, `PhoenixTextArea`, `PhoenixSelectField`, `PhoenixCheckbox`, `PhoenixRadio`, `PhoenixRadioGroup`, `PhoenixToggle`, `PhoenixDatePicker`, `PhoenixDateSelect`, `PhoenixPlusMinus`, `PhoenixField`

### Overlays & Dialogs

`PhoenixModal`, `PhoenixDrawer`, `PhoenixTooltip`, `PhoenixPopper`, `PhoenixBottomSheet`, `PhoenixDatePopper`

### Navigation

`PhoenixHeaderBar`, `PhoenixHeaderBarUtility`, `PhoenixTabs`, `PhoenixTab`, `PhoenixAnchorNavigation`, `PhoenixBreadcrumb`, `PhoenixMenuVertical`, `PhoenixPagination`, `PhoenixStepper`, `PhoenixStep`

### Feedback & Status

`PhoenixAlert`, `PhoenixSnackbarManager`, `PhoenixSnackbarMessage`, `PhoenixSpinner`, `PhoenixProgressBar`, `PhoenixRating`

### Cards & Content

`PhoenixCard`, `PhoenixProductCard`, `PhoenixTile`, `PhoenixTileContent`, `PhoenixBanner`, `PhoenixDealBar`, `PhoenixDealPromotionCard`, `PhoenixAccordion`, `PhoenixAccordionItem`, `PhoenixExpandableSection`, `PhoenixSpotlight`

### Media & Carousels

`PhoenixIcon`, `PhoenixImagery`, `PhoenixGallery`, `PhoenixVideo`, `PhoenixCarouselResponsive`, `PhoenixCarouselStatic`, `PhoenixPicture`

### Lists & Data

`PhoenixDataTable`, `PhoenixPointList`, `PhoenixPointListItem`, `PhoenixIconList`, `PhoenixIconItem`, `PhoenixReview`

### Actions & Links

`PhoenixButton`, `PhoenixAppLink`, `PhoenixChip`, `PhoenixSeparator`, `PhoenixPrice`

### Travel-Specific

`PhoenixBoatCard`, `PhoenixCardDeparture`, `PhoenixCardFlight`, `PhoenixProfileCard`, `PhoenixTripDetailsCard`

---

## SCSS Pattern Essentials

```scss
// Import abstracts at top of component .scss
@import '../../styles/themes/phoenix-v2/abstracts/variables';
@import '../../styles/themes/phoenix-v2/abstracts/mixins';

.pnx-my-component {
  color: var(--pnx-ui-palette-text-text-primary); // CSS custom prop for themeable values
  padding: $spacing-m; // SCSS variable for build-time values
  background: $brand-primary-sand;

  @include breakpoint('md') {
    padding: $spacing-l;
  }

  @include shadow(2); // elevation
  @include transition(opacity); // animation

  &--disabled {
    opacity: 0.3; // $opacity-disabled token value
  }
}
```

**Utility classes** follow `pnx-{[breakpoint]:}{group}--{value}`:

- `pnx-margin--m`, `pnx-padding-top--s`, `pnx-md:display--flex`
- `pnx-text-color--primary-intrepid-red`, `pnx-bg-color--primary-sand`
- `pnx-visually-hidden`, `pnx-sr-only`, `pnx-focus-outline`

Responsive breakpoint utilities use colon syntax in HTML: `pnx-md:margin--m`.

---

## TypeScript / Vue Pattern

```vue
<script setup lang="ts">
const props = withDefaults(
  defineProps<{
    label: string
    variant?: 'primary' | 'secondary'
    disabled?: boolean
  }>(),
  {
    variant: 'primary',
    disabled: false,
  },
)

const emit = defineEmits<{
  click: [event: MouseEvent]
  update: [value: string]
}>()
</script>

<template>
  <button
    class="pnx-button"
    :class="`pnx-button--${props.variant}`"
    :disabled="props.disabled"
    @click="emit('click', $event)"
  >
    <slot />
  </button>
</template>
```

Component file location: `src/components/<Name>/<Name>.vue`. Export in `src/index.ts`. Add stories in `*.stories.ts`.

---

## Quick Commands

```bash
yarn dev           # Storybook dev server (localhost:6006)
yarn lint          # Biome + Stylelint + ESLint
yarn unit:test     # Jest unit tests
yarn integration:run  # Cypress headless
yarn build:library # Build dist-library/
# Token export: PHOENIX-TOKENS.json (committed to repo, no script needed)
```

Node 22+ LTS. Yarn 4 (Berry) package manager.

---

## Accessibility Checklist

- All actionable elements keyboard-reachable and operable
- Visible focus styles (`pnx-focus-outline` or custom)
- Native elements first; ARIA only where necessary
- WCAG AA contrast across all active themes
- Respects `prefers-reduced-motion`
- Interactive components tested with axe in Cypress

---

## Additional Resources

- **`references/tokens.md`** — Full token tables: all 150+ CSS custom properties, spacing, typography, breakpoints, motion, shadows, z-index, mixins reference
- **`references/components.md`** — Complete component API: all 68+ components with props, emits, slots, accessibility notes grouped by category
- **`references/cross-platform.md`** — Mobile (SwiftUI/Compose/React Native/Flutter), email, Salesforce LWC, AI chatbot guides with working code snippets
