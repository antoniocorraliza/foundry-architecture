# 🛠️ Foundry support hub

Official frontend application for the **Foundry support hub**, an **enterprise SaaS & PWA** for support ticket and user management. Built with **Angular**, this client leverages modern reactive paradigms (Signals), Progressive Web App (PWA) capabilities, and a custom UI component library to deliver a fast, secure, and highly interactive user experience.

<div align="center">
  <p><b>🖥️ Desktop enterprise workspace</b></p>
  <img src="https://5e6779dd-1707-4644-ade6-8d2814c48f97.clouding.host/public/images/foundry-support-hub.gif" width="100%" alt="Foundry desktop preview" style="border-radius: 8px; border: 1px solid #1e293b; max-width: 850px;">

  <p style="margin-top: 32px;"><b>📱 Mobile PWA & Push notifications</b></p>
  <img src="https://5e6779dd-1707-4644-ade6-8d2814c48f97.clouding.host/public/images/foundry-support-hub-mobile.gif" width="280" alt="Foundry mobile PWA preview" style="border-radius: 8px; border: 1px solid #1e293b;">

</div>

## 🔐 Authentication, Security & Routing

- **Reactive route guards**: Implementation of `authGuard`, `publicGuard`, and `roleGuard` to strictly protect private modules, prevent authenticated users from accessing public login views, and restrict administrative routes exclusively to users with `ADMIN` privileges.

- **JWT interception & refresh**: Seamless token injection and automated, silent token refreshing (`FoundryRefreshTokenProvider`) using HTTP Interceptors to maintain active sessions without interrupting the user workflow.

- **Real-time session invalidation**: WebSocket listener integrated into the global layout that reacts to `force_logout` events. If an administrator modifies a user's role or blocks their account, the client instantly clears local storage and forces a redirection to the login screen.

- **Role-based UI rendering & access (RBAC)**: Intelligent frontend stores and route guards that evaluate the user's `ADMIN` or `USER` profile on the fly, dynamically hiding destructive actions (e.g., bulk deletions), administrative menus, sensitive routing paths, and blocking unauthorized route access.

## 📱 Core architecture & UX

- **Signal based state management**: Modular, localized state management utilizing Angular's `WritableSignal`, `computed`, and `effect` primitives (e.g., `TicketManagementStore`, `DashboardStore`) for highly performant, zone-less change detection.

- **Smart API request dispatcher**: Centralized HTTP request handler featuring a "cooldown" cache system. It intercepts grouped backend errors (e.g., multiple 404s or 500s occurring simultaneously) and prevents notification spam, ensuring the user only sees a single, clean toast message.

- **Responsive layouts**: Adaptive structure featuring a dynamic Sidebar for desktop and a custom Hamburger menu for mobile devices, automatically switching views and limiting data density based on the viewport.

## 🎫 Tickets module

The core operational view for tracking and resolving support requests:

- **Dual view system**: Seamless toggling between a highly interactive Kanban Board (with Drag & Drop capabilities for state updates) and a comprehensive Data Table view.

- **Client side file processing**: Native frontend parsing of files into Base64 format (`FileStorageUtil` equivalents) before submission, enforcing strict MIME-type and size validations (Max 10MB) for documents, images, and code snippets.

- **Advanced attachment previewer**: Custom dialog component (`AttachmentPreviewDialogComponent`) capable of rendering uploaded images, decoding Base64 files, and embedding PDFs securely within iframes, including mobile-specific optimizations.

- **Contextual actions**: Action bars and dynamic dropdowns for filtering by priority, type, and status, executing batch CSV exports, and launching modal-driven edits.

## 👥 Users module

Administrative interface for team and access management:

- **Interactive directory**: Paginated data tables with reactive search debouncing, custom cell rendering for user avatars (falling back to initials), and status indicators.

- **Secure modals**: Action dialogs for high-stakes operations such as role promotion/demotion, password resets, and account blocking, providing clear descriptive warnings before execution.

- **Batch operations**: Multi-selection capabilities allowing administrators to export or delete multiple users directly from the UI.

## 📊 Dashboard & Analytics

Data visualization center for performance tracking:

- **ECharts integration**: Embedded `ngx-echarts` directives for rendering interactive Pie charts (Status), Bar charts (Type & Priority), and Line graphs (Version tracking).

- **Reactive date filtering**: Built-in calendar components that instantly trigger API refetches to update all KPIs and graphics based on selected date ranges.

- **Dynamic KPI cards**: Highlights critical metrics such as "Stale tickets (> 14 days)" and "Pending actions" with visual severity indicators.

## 🔔 PWA & Notifications module

Native-like notification and installation capabilities:

- **Progressive web app (PWA)**: Fully installable application with manifest configuration, custom splash screens, and offline network status tracking (`NetworkStatusService`). Includes custom installation banners specifically tailored for both Android/Desktop and iOS (Share -> Add to Home Screen).

- **Web push API**: Integration with `@angular/service-worker` (`SwPush`) to prompt and store VAPID-based push subscriptions, receiving background notifications even when the browser is closed.

- **Badge API**: Automatic syncing of unread notification counts with the operating system's app icon badge (`navigator.setAppBadge`).

- **Live sockets**: Active Socket.IO connection that triggers real-time toast alerts across the UI without requiring page reloads, keeping the team synchronized.

- **Deep linking handling**: Intercepts payload URLs from push notifications, parsing query parameters to open specific ticket or user modals instantly upon clicking the alert.

- **Offline-first caching engine**: Advanced encryption-backed local storage caching utility (`OfflineCacheService`) that gracefully intercepts network failures and serves fallback data with custom notification cooldowns.

- **Comprehensive PWA lifecycle management**: Dedicated services handling automated version update checks and dialog notifications (`PwaUpdateService`), install prompt orchestration (`PwaInstallService`), and badge synchronization (`PwaBadgeService`).

- **Hybrid iOS-optimized update strategy**: Platform-aware lifecycle orchestration via precise device fingerprinting. It provides seamless automated updates for Android and desktop platforms while gracefully avoiding WebKit's IPC communication constraints on iOS through background activation and guided manual restarts, ensuring long-term deep-link and push-notification stability.

## 📄 License

Property of **Antonio Corraliza León** as part of the Foundry development suite. All rights reserved.

