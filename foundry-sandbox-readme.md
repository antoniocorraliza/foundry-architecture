# 🚀 Foundry sandbox

> **[🚀 Explore the live application](https://foundry-sandbox.vercel.app/)**  
> _Interactive execution, real-time component evaluation, and live technical specifications for the entire Foundry suite._

The **Foundry sandbox** is the official interactive documentation and component showcase for the complete Foundry suite. Built on a modular **Angular** architecture, it serves as a live environment where engineers can explore, configure, and test components, directives, utilities, and core services in real-time.

## ⚙️ Key features

- **Interactive documentation:** Real-time component visualization using demo cards, control panels, code viewers, JSON viewers, and API previews.

- **Advanced responsive architecture:** Precise adaptive layout featuring dynamic lateral navigation for desktop and touch-friendly overlay menus for mobile.

- **High performance & reactivity:** Built with strict change detection (`ChangeDetectionStrategy.OnPush`), modern dependency injection, and clean reactive state management.

- **Consistent design system:** Native integration via global CSS variables providing absolute control over themes while keeping base styles independent.

- **Accessibility & UX:** Optimized for a native-like experience with automatic scroll restoration and suppression of unwanted mobile behaviors.

## 🛡️ Anti-spam & security layer

Silent, CSS-hidden honeypot traps and temporal rate-limiting (cooldown) engineered to prevent automated bot scraping and request flooding without introducing user-facing friction.

## 🏛️ Architecture & suite structure

The **Foundry sandbox** integrates and exercises the three core enterprise pillars of the suite:

### 🧠 Foundry core

- **Configuration:** Immutable runtime configuration management via `FoundryConfigurationService`.

- **Constants:** Strictly typed enumerations, HTTP status codes (`FoundryHttpStatus`), request headers, and standardized error messages (`FoundryNetworkMessages`).

- **Error handling:** Application-wide safety net via `FoundryGlobalErrorHandler`.

- **Network:** High-performance communication layer featuring `FoundryHttpClientService`, `ApiRequestDispatcherService`, and interceptors with context token bypasses.

- **Routing:** Advanced navigation controller (`FoundryRouterService`) wrapping Angular Router and Location.

- **Security:** Authentication architecture featuring `foundryAuthRefreshInterceptor` with mutex-locked queueing, `FoundryRefreshTokenProvider`, `foundryJwtInterceptor`, and `FoundryTokenService`.

- **State management:** Real-time cross-tab synchronization via `FoundryBroadcastChannelService`.

- **Storage:** Secure browser storage wrapper (`FoundryBrowserStorageService`) supporting local and session persistence.

- **User interface:** Dynamic visual engine for modal dialogs (`FoundryDialogWindowService`), notifications (`FoundryNotificationService`), and loading indicators.

### 🧰 Foundry utils

- **API normalization**: Recursive transformation of backend `snake_case` properties (`\_id`) into frontend `camelCase`.

- **Common utils**: Unique ID generation, secure UUID v4 creation, random alphanumeric codes, and asynchronous execution delays (`sleep`).

- **Crypt utils**: Character-by-character hexadecimal string encoding and decoding.

- **CSV utils**: Automated browser CSV downloads with column mappings and asynchronous parsing (`importFromCsv`).

- **Date utils**: Temporal logic engine supporting intervals, calendar grids (`getDaysBy`), and ISO week calculations.

- **Debounce utils**: Performance optimization tools providing global simple debouncers and independent form input tracking.

- **Form data utils**: Safe factory construction of multipart payloads (`setFormData`) combining text fields and binary streams.

- **Format utils**: Formatters for currency, URL-friendly slugs, text truncation, string capitalization, and boolean normalization.

- **Hash utils**: Asynchronous cryptographic hashing (`sha256`, `sha512`) via the native Web Crypto API (`crypto.subtle`).

- **Object utils**: Deep object cleaning, immutable cloning (`cloneObject`), and property difference detection (`getObjectDifferences`).

- **Validation utils**: Mathematical and regular expression verifications including Spanish DNI modulus calculation, email checks, and password strength.

### 🎨 Foundry UI

- **Constants:** Type-safe sort directions (`FoundrySortDirection`) and standardized icon registries.

- **Core elements:** Atomic building blocks (`FoundryButtonComponent`, `FoundryChipComponent`, `FoundryTypographyComponent`) optimized with OnPush.

- **Directives:** Declarative DOM enhancements including drag-and-drop, portals, click-outside detection, file inputs, and tooltips.

- **Forms:** Unified data entry components implementing `ControlValueAccessor` and `Validator`.

- **Layouts:** Macro-architectural containers (`FoundrySidebarLayoutComponent`, `FoundryHeaderLayoutComponent`).

- **Managers:** Global UI state controllers like `FoundrySidebarStateService`.

- **Pipes:** Template transformations including `FoundrySanitizeXssPipe`.

- **Widgets:** Composite components including responsive RBAC sidebars, breadcrumbs, toolbars, and advanced data tables (`FoundryTableComponent`).

## 💻 Technologies & stack

- **Framework:** Angular 19+ (TypeScript, HTML, SCSS).

- **Styling:** CSS custom properties and custom SASS mixins..

- **Architecture:** Component-driven design, reactive patterns with RxJS, and zero-dependency utility logic.

## 📄 License

Property of **Antonio Corraliza León** as part of the Foundry development suite. All rights reserved.

