# 🏭 Foundry suite

A modular, zero-dependency enterprise architecture and component suite designed for Angular 19+ applications.

[![Angular](https://img.shields.io/badge/Angular-19.2+-DD0031?style=for-the-badge&logo=angular)](#)
[![TypeScript](https://img.shields.io/badge/TypeScript-Ready-3178C6?style=for-the-badge&logo=typescript)](#)
[![Zero dependency](https://img.shields.io/badge/Dependencies-0-06b6d4?style=for-the-badge)](#)
[![License](https://img.shields.io/badge/License-Proprietary-0f172a?style=for-the-badge)](#license)

> **[🚀 Live demo: Explore The Foundry sandbox](https://foundry-sandbox.vercel.app/)**

### 📦 Official NPM packages

- [**@antoniocorraliza/foundry-core**](https://www.npmjs.com/package/@antoniocorraliza/foundry-core)

- [**@antoniocorraliza/foundry-ui**](https://www.npmjs.com/package/@antoniocorraliza/foundry-ui)

- [**@antoniocorraliza/foundry-utils**](https://www.npmjs.com/package/@antoniocorraliza/foundry-utils)

## 🌐 Overview

**Foundry suite** is an architectural suite structured to handle state, networking, UI orchestration, and core data processing in modern Angular applications. By decoupling business logic from the visual layer, the suite enforces architectural consistency, eliminates boilerplate code, and optimizes rendering performance without relying on heavy third-party UI frameworks.

## 🎯 Engineering rationale

Building a custom Angular architecture instead of relying on traditional third-party monoliths (such as Angular Material or the CDK) addresses three core architectural bottlenecks in large-scale applications:

1. **Bundle size and performance:** Avoiding heavy external UI dependencies to maintain fine-grained control over DOM manipulation and render cycles (`OnPush`).

2. **Separation of concerns:** Strictly isolating cross-functional infrastructure (`core`), visual orchestration (`ui`), and framework-agnostic data processing (`utils`) to eliminate tight coupling.

3. **Boilerplate reduction:** Centralizing complex logic—such as JWT concurrency queues, cross-tab synchronization, and reactive form state management—to prevent repetitive, error-prone code across enterprise modules.

## 🏛️ Architecture & suite structure

The suite is split into three core pillars, separating infrastructure, visual components, and framework-agnostic data logic:

### 🧠 1. Foundry core

**The cross-functional infrastructure layer.** Foundry core provides a robust backend-frontend integration backbone, handling network communication, global state, and lifecycle services.

- **Network orchestration**: HTTP client wrapper featuring automated prefixing, global loading indicators, and a mutex-locked queueing interceptor (`foundryAuthRefreshInterceptor`) to prevent concurrent token-refresh collisions.

- **Security & Session:** JWT lifecycle management, token providers, and real-time cross-tab synchronization using the native `BroadcastChannel` API coupled with `DestroyRef` for memory safety.

- **UI Services**: Dynamic component rendering engines injected directly into the DOM for multi-dialog stacking (`FoundryDialogWindowService`) and toast notifications (`FoundryNotificationService`).

- **Configuration & Error handling:** Deeply frozen runtime configuration (`FoundryConfigurationService`) and an application-wide global error handler (`FoundryGlobalErrorHandler`).

### 🎨 2. Foundry UI

**The visual orchestration layer.** A strictly standalone, Material-free component library built for high-density enterprise dashboards.

- **Performance-driven rendering:** Every component implements `ChangeDetectionStrategy.OnPush` and uses content projection (`ng-content`) to avoid rigid inheritance patterns.

- **Design system**: Pure SCSS design tokens and native CSS custom properties for instant theme configuration without compilation overhead.

- **Directives & Widgets**: Custom hardware-accelerated Drag & Drop wrappers, portaling APIs, form controls implementing `ControlValueAccessor`, and advanced composite data tables.

### 🧰 3. Foundry utils

**The framework-agnostic data processing core.** A pure TypeScript utility library completely isolated from UI frameworks, enabling reuse across Node.js services, web workers, or alternative frontends.

- **Data normalization:** Recursive conversion between `snake_case` backend properties and camelCase frontend models.

- **Temporal & Cryptographic logic**: Advanced date manipulation engines, secure Web Crypto hashing (`crypto.subtle`), and CSV bidirectional parsing.

- **Validation & Object manipulation**: Strict validators (DNI/NIE, custom formats) and deep object cloning, cleaning, and difference detection without external dependencies.

## 🧪 Validation via 'Dogfooding'

The suite validates structural contracts and rendering performance through direct integration across two internal architectural environments:

1. **Foundry support hub:** An enterprise Software as a Service (SaaS) and Progressive Web App (PWA) environment executing ticket telemetry, user access control, and state management via an Angular client and a NestJS/Prisma API backend.

2. **Foundry sandbox:** An interactive documentation runtime executing real-time component evaluation, dependency injection testing, and utility configuration.

The following architectural diagram defines the macroscopic topology of this ecosystem. It details the consumption of zero-dependency client libraries and the integration vectors with browser native APIs, real-time backend infrastructures, and external service providers.

<div align="center">
  <img src="https://5e6779dd-1707-4644-ade6-8d2814c48f97.clouding.host/public/images/arquitecture-diagram.png" width="100%" alt="Foundry ecosystem architecture" style="border-radius: 8px; border: 1px solid #1e293b; max-width: 850px; margin: 24px 0;">
</div>

### Architectural implementation contracts

- **Compile-time infrastructure:** The NPM modules (`@foundry-core`, `@foundry-ui`, and `@foundry-utils`) execute UI orchestration, data normalization, and network interception strictly as compile-time dependencies, enforcing architectural isolation without runtime bloat.

- **Offline execution and PWA resilience:** The client layer implements native browser API protocols. The Service Worker (`@angular/service-worker`) intercepts background push payloads, while a secure offline cache engine persists JWT credentials to guarantee data availability during network degradation.

- **Cross-tab synchronization:** The architecture coordinates global application state across multiple browser execution contexts in real-time utilizing the native `BroadcastChannel` API, mitigating session inconsistencies and bypassing redundant network payload generation.

- **Dual network pipeline:** Client-server communication vectors are strictly decoupled. JWT lifecycle operations and standard data transmission follow deterministic HTTP/REST pipelines, whereas server-sent events (including push notifications and `force_logout` administrative actions) execute via concurrent, authenticated WebSockets.

## 🚀 Getting started

The libraries in the suite are natively optimized for Angular 19+ and utilize modern standalone architecture.

### 1. Installation via NPM

To deploy and integrate the full Foundry suite into your Angular project, run the following command in the terminal of your development environment:

```bash
npm i @antoniocorraliza/foundry-utils @antoniocorraliza/foundry-ui @antoniocorraliza/foundry-core
```

If, for architectural reasons, you prefer to install only specific modules, you can add them individually:

**Foundry utils**

```bash
npm i @antoniocorraliza/foundry-utils
```

**Foundry UI**

```bash
npm i @antoniocorraliza/foundry-ui
```

**Foundry core**

```bash
npm i @antoniocorraliza/foundry-core
```

### 2. Dependencies and versions

The suite relies on a strict baseline of native dependencies to guarantee operational stability. To set up the environment, you need to have Angular CLI 19+ (`^19.2.19` or later) installed.

| PACKAGE                 | REQ. VERSION     | PURPOSE IN THE SUITE                                     |
| :---------------------- | :--------------- | :------------------------------------------------------- |
| **Node.js**             | `v18.13+ / v20+` | Compatible with the LTS versions required by Angular 19. |
| **tslib**               | `^2.3.0`         | Native support for build helpers in TypeScript.          |
| **@angular/common**     | `^19.2.0`        | Required by Foundry UI and Foundry core.                 |
| **@angular/core**       | `^19.2.0`        | Required by Foundry UI and Foundry core.                 |
| **@angular/animations** | `^19.2.0`        | Orchestrate smooth transitions between visual elements.  |
| **@angular/forms**      | `^19.2.0`        | How the control model works (ControlValueAccessor).      |

### 3. Design system and tokens

To ensure visual consistency, Foundry UI centralises its styling using design tokens. Import the global styles into your main `src/styles.scss` file:

```scss
@use "@antoniocorraliza/foundry-ui/styles" as *;
```

### 4. Configuring the main provider

To enable the core infrastructure to start operating automatically in your Angular application, register the interceptors in your `app.config.ts`:

```typescript
export const appConfig: ApplicationConfig = {
  providers: [
    provideHttpClient(
      withInterceptors([
        // 1. Global loader: Handles all network activity
        foundryLoaderInterceptor,
        // 2. Auth refresh: Handles the 401 error and retries the request
        foundryAuthRefreshInterceptor,
        // 3. JWT interceptor: Injects the updated token
        foundryJwtInterceptor,
        // 4. API prefix: Adds the base URL to the outgoing request
        foundryApiPrefixInterceptor("[https://api.foundry-suite.com](https://api.foundry-suite.com)"),
      ]),
    ),
    // Provider required for the abstract token refresh class
    {
      provide: FoundryRefreshTokenProvider,
      useExisting: YourLocalRefreshTokenProvider,
    },
    // Global exception handler
    { provide: ErrorHandler, useClass: FoundryGlobalErrorHandler },
  ],
};
```

## 📄 License

Property of **Antonio Corraliza León** as part of the Foundry development suite. All rights reserved.

