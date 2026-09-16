# 🏗️ Foundry UI

The visual orchestration layer. A strictly standalone, zero-dependency Angular UI library built for maximum performance and scalable enterprise applications.

[![npm version](https://img.shields.io/npm/v/@antoniocorraliza/foundry-ui?color=a3e635&style=for-the-badge&logo=npm)](https://www.npmjs.com/package/@antoniocorraliza/foundry-ui)
[![Angular](https://img.shields.io/badge/Angular-19.2+-DD0031?style=for-the-badge&logo=angular)](https://angular.dev/)
[![License](https://img.shields.io/badge/License-Proprietary-0f172a?style=for-the-badge)](#license)
[![Zero dependency](https://img.shields.io/badge/Dependencies-0-06b6d4?style=for-the-badge)](#)

## 🌐 Overview

**Foundry UI** is the visual orchestration layer and design system of the Foundry suite. Designed from the ground up for modern Angular applications, it completely abandons monolithic frameworks (100% Material-free) in favor of a strictly decoupled, highly performant, and reactive architecture.

It provides a comprehensive set of UI components, form controls, advanced widgets (such as data tables and drag & drop systems), and layout orchestrators—all driven by a robust CSS Design Token system.

## ⚙️ Key features & design philosophy

- **Zero dependencies:** Completely self-contained with no external UI library bloat.

- **Strictly standalone:** Modern Angular architecture enabling precise, tree-shakeable imports.

- **Maximum performance:** Built with `ChangeDetectionStrategy.OnPush` to guarantee fluid rendering in high-density enterprise dashboards.

- **Composition over inheritance:** Relies heavily on `<ng-content>` projection to maintain clean, flexible layouts.

- **Native CSS tokens:** SCSS and CSS variable-driven design system allowing instant global overrides without compilation overhead.

- **Reactive orchestration:** Layouts and widgets communicate via reactive state services, eliminating prop-drilling.

## 📦 Installation & Setup

Install the package via npm:

```bash
npm install @antoniocorraliza/foundry-ui
```

### Setup styles

Import the global styles into your application's root stylesheet (`src/styles.scss`) to load design tokens, fonts (`Inter`, `Urbanist`), and Google Material Symbols Outlined:

```scss
/* src/styles.scss */
@use "@antoniocorraliza/foundry-ui/styles" as *;
```

## 🧩 Architecture & ecosystem

The library is structured into 8 core architectural pillars:

- **Constants**: Static configurations, view definitions, and standardized icon registries (`FoundryCommonIcon`).

- **Core elements**: Atomic building blocks (`FoundryButtonComponent`, `FoundryChipComponent`, `FoundryTypographyComponent`) optimized for minimal memory usage.

- **Directives**: Hardware-accelerated DOM enhancements including `FoundryDragDirective`, `FoundryDropListDirective`, `FoundryPortalDirective`, and `FoundryTooltipDirective`.

- **Forms**: Unified data entry components implementing `ControlValueAccessor` and `Validator`, featuring custom calendars, auto-grow textareas, and touch-optimized signature capture (`foundry-draw-box`).

- **Layouts**: Macro-architectural containers (`FoundrySidebarLayoutComponent`, `FoundryHeaderLayoutComponent`) utilizing semantic slots.

- **Managers**: Global UI state controllers utilizing RxJS `BehaviorSubject` for synchronized layout management.

- **Pipes**: Secure template data transformations including `FoundrySanitizeXssPipe` leveraging Angular's `DomSanitizer`.

- **Widgets**: Compound components including RBAC-filtered multi-level sidebars, breadcrumbs, toolbars, and advanced data tables (`FoundryTableComponent`).

## 🎨 Theming & customization

To customize the global visual tokens, override the root CSS variables and SASS maps after importing the library styles:

```scss
@use "@antoniocorraliza/foundry-ui/styles" as *;

:root {
  --foundry-background-main: #020617;
  --foundry-background-card: #0f172a;
  --foundry-border: #1e293b;
  --foundry-border-hover: #334155;
  --foundry-accent: #a3e635;
  --foundry-text-primary: #f8fafc;
  --foundry-text-secondary: #cbd5e1;
  --foundry-error: #ef4444;
  --foundry-warning: #f59e0b;
  --foundry-info: #06b6d4;
  --foundry-success: var(--foundry-accent);
  --foundry-font-heading: "Urbanist", sans-serif;
  --foundry-font-body: "Inter", "Arimo", sans-serif;
  --foundry-font-weight-light: 300;
  --foundry-font-weight-regular: 400;
  --foundry-font-weight-medium: 500;
  --foundry-font-weight-semibold: 600;
  --foundry-font-weight-bold: 700;
  --foundry-font-weight-extrabold: 800;
  --foundry-font-weight-heavy: 900;
  --foundry-radius-mini: 4px;
  --foundry-radius-small: 8px;
  --foundry-radius-big: 16px;
  --foundry-shadow-card: 0px 4px 6px -1px rgba(0, 0, 0, 0.5);
  --foundry-opacity-disabled: 0.4;
  --foundry-z-base: 1;
  --foundry-z-sticky: 100;
  --foundry-z-dropdown: 200;
  --foundry-z-backdrop: 300;
  --foundry-z-modal: 400;
  --foundry-z-tooltip: 500;
  --foundry-z-loader: 600;
  --foundry-z-notifications: 700;
  --foundry-z-drag: 800;
}

$foundryBreakpoints: (
  sm: 640px,
  md: 768px,
  lg: 1024px,
  xl: 1280px,
);
```

### Utility SASS mixins

The suite exports mixins that are ready to be included in your custom components using `@include`:

- **`@include foundryCustomScrollbar;`** – Custom scrollbar styling.

- **`@include foundryDisabledState;`** – Disabled opacity, event blocking, and not-allowed cursor.

- **`@include foundryRespondTo(breakpoint);`** – Responsive control for breakpoints (sm, md, lg, xl).

- **`@include foundrySidebarActiveState;`** – Active styling and accent indicator bar for navigation items.

- **`@include foundryGlassBackdrop;`** – Semi-transparent blurred backdrop style for overlays.

## 💻 Integration examples

For advanced use cases and fully developed code integration examples, visit the official documentation portal:

**🌐 [https://foundry-sandbox.vercel.app/foundry-ui](https://foundry-sandbox.vercel.app/foundry-ui)**

## 🛡️ Peer dependencies

- `@angular/core`: `>=19.2.0`

- `@angular/common`: `>=19.2.0`

- `@angular/forms`: `>=19.2.0`

- `@angular/animations`: `>=19.2.0`

## 📄 License

Property of **Antonio Corraliza León** as part of the Foundry development suite. All rights reserved.

