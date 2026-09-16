# 🧠 Foundry core

The foundational infrastructure and core architecture for Angular enterprise applications.

[![npm version](https://img.shields.io/npm/v/@antoniocorraliza/foundry-core?color=a3e635&style=for-the-badge&logo=npm)](https://www.npmjs.com/package/@antoniocorraliza/foundry-core)
[![Angular](https://img.shields.io/badge/Angular-19.2+-DD0031?style=for-the-badge&logo=angular)](https://angular.dev/)
[![License](https://img.shields.io/badge/License-Proprietary-0f172a?style=for-the-badge)](#license)
[![Zero dependency](https://img.shields.io/badge/Dependencies-0-06b6d4?style=for-the-badge)](#)

## 🌐 Overview

**Foundry core** is an enterprise-grade, Material-free infrastructure and UI core library designed for Angular applications. Acting as the foundational backbone of the Foundry suite, it provides a robust architecture for networking, security, global state, and dynamic UI components without relying on heavy third-party frameworks.

## ⚙️ Key features & design philosophy

- **Material-free:** 100% native Angular DOM manipulation (`createComponent`, `ApplicationRef`), completely bypassing Angular Material and the CDK.

- **Enterprise-ready:** Built-in memory leak prevention, RxJS reactivity, Zone.js optimizations (`runOutsideAngular`), and advanced concurrency controls.

- **Plug & play:** Ready-to-use default components (such as confirmation dialogs and loaders) requiring zero HTML boilerplate.

- **SSR compatible:** Safely interacts with the DOM using Angular environment injectors for Server-Side Rendering compliance.

## 🧩 Architecture & modules

The library is organized into cohesive modules handling critical infrastructure logic:

- **Network**: Advanced HTTP client (`FoundryHttpClientService`) featuring automated request dispatching, standardized error mapping, and interceptors (API prefixing, auto-loader, and mutex-locked token refresh).

- **Security**: Comprehensive JWT management, authentication contexts, and a plug-and-play refresh token provider (`FoundryRefreshTokenProvider`).

- **User interface**: Dynamic, zero-dependency UI managers for Modals (`FoundryDialogWindowService`), Notifications (`FoundryNotificationService`), and global loaders directly injected into the DOM.

- **State**: Cross-tab synchronization via `FoundryBroadcastChannelService` utilizing native `BroadcastChannel` APIs.

- **Storage**: Strictly typed, serialized browser storage engine wrapper (`FoundryBrowserStorageService`).

- **Config & errors**: Runtime application configuration loading (`FoundryConfigurationService`) and a global error handler (`FoundryGlobalErrorHandler`).

- **Routing**: Robust navigation wrapper (`FoundryRouterService`) managing query parameters, navigation state, and deep routing.

## 💻 Integration Examples

For advanced use cases and fully developed code integration examples, visit the official documentation portal:

**🌐 [https://foundry-sandbox.vercel.app/foundry-core](https://foundry-sandbox.vercel.app/foundry-core)**

## 🛡️ Peer dependencies

This suite is built on top of the latest Angular features. Make sure your environment satisfies the following:

- `@angular/core`: `>=19.2.0`

- `@angular/common`: `>=19.2.0`

## 📄 License

Property of **Antonio Corraliza León** as part of the Foundry development suite. All rights reserved.

