# 🛠️ Foundry support hub API

Official collection for interacting with the **Foundry support hub** backend, an enterprise system built on **NestJS, Prisma, and SQLite/LibSQL**. This API provides a robust engine for user management, role control, technical support ticket tracking, and data analytics.

## 🔐 Authentication and security

- **Dual-layer JWT authentication:** Implements a secure system of _Access Token_ (short-lived) and _Refresh Token_ (long-lived with encrypted database storage).
- **Postman automation:** The `Login` and `Refresh tokens` endpoints include test scripts that **automatically capture the tokens** and inject them into the collection variables (`{{access_token}}` and `{{refresh_token}}`). Zero manual copy-pasting!
- **Access control (RBAC):** Strict role system (`ADMIN` and `USER`). Admin routes automatically block any unauthorized access attempt by returning a `403 Forbidden`.
- **Rate limiting:** Active defenses against brute-force attacks using `@nestjs/throttler` (e.g., maximum of 5 login attempts per minute).

## 👥 Users module

Advanced administration and profile system:

- **Exploration:** Paginated listings with combinable filters (`search`, `isBlocked`), offset (`offset`), and dynamic sorting (`sortBy`, `sortOrder`).
- **Data export:** Dedicated `/export` endpoint designed to retrieve full unpaginated datasets for administrative reporting and backup purposes.
- **Account security:** Isolated endpoints for password updates and temporary user blocking/banning system (`toggle-block`).
- **Roles:** Account promotion and demotion (`updateRole`) protected exclusively for administrators.
- **File processing:** Native support for decoding and storing profile images (`profileImage`) sent in Base64 format.

## 🎫 Tickets module

Core of the incident reporting and support system:

- **Strict life cycle:** Status control using Enums (`PENDING`, `IN_PROGRESS`, `RESOLVED`, `CLOSED`).
- **Triaging & Priority:** Advanced priority system (`UNCLASSIFIED`, `LOW`, `MEDIUM`, `HIGH`, `CRITICAL`) managed via a strictly isolated endpoint (`PATCH /:id/priority`) for fine-grained access control and precise filtering.
- **Kanban synchronization:** Atomic status updates (`updateStatus`) that synchronize both the ticket's `status` and its visual `position` within columns using Prisma database transactions.
- **Data export:** Dedicated `/export` endpoint for generating complete, unpaginated ticket reports.
- **Evidence and attachments:** Complex upload system for file attachments linked to tickets (images, PDFs, documents), decoding Base64 and physically storing them on the server.
- **Bulk operations:** Optimized endpoints (`/batch`) to allow administrators to clean or delete multiple tickets/users in a single transaction.
- **Optimized selectors:** Lightweight routes (`/selector`) designed with the sole purpose of mapping basic data (ID and Subject) to render ultra-fast dropdowns in the frontend.

## 📊 Statistics module

Advanced data aggregation engine designed to power administrative dashboards:

- **Real-time metrics:** Aggregated data for ticket volume, status breakdown, and categorization executing Prisma `groupBy` and `count` operations without loading raw records into memory.
- **Advanced date filtering:** Precise date range capabilities (`startDate` and `endDate`) automatically handled, validated, and normalized to full UTC days to prevent data loss.
- **Technical impact analysis:** Specialized endpoints to group bugs and issues by software versions (`foundryCoreVersion` and `angularCliVersion`), enabling immediate impact assessment.
- **SLA tracking (Stale tickets):** Dedicated monitoring for tickets stuck in `PENDING` or `IN_PROGRESS` for over 14 days, preventing bottlenecks in the support queue.
- **Chart-ready responses:** Intelligent data formatting that pre-fills missing categorizations with zero-values, guaranteeing strict JSON structures for predictable rendering in frontend charting libraries (Chart.js, ECharts, etc.).

## 🔔 Notifications module

Real-time push notification engine and persistent alerts system:

- **Web Push integration (PWA):** Full support for background notifications via VAPID (`/push/subscribe`, `/push/unsubscribe`). Delivers native OS alerts with custom badges, vibration patterns, and interactive action buttons, even when the application is closed.
- **Deep linking & Contextual routing:** Push payloads dynamically calculate target URLs and inject entity identifiers (e.g., `ticketId`, `userSearch`), allowing users to click an alert and jump directly to the exact ticket or profile in the frontend.
- **Real-time WebSockets:** Powered by Socket.IO (`/ws/notifications`), enabling instant delivery of in-app alerts. Connections are securely authenticated using JWT via the handshake payload, automatically isolating users in private WebSocket rooms.
- **Persistent history:** Database-backed notifications using Prisma. Ensures users never miss an alert, capturing the state (`isRead`) even if they are offline when the event occurs.
- **Advanced batch management:** Comprehensive bulk operations to mark multiple alerts as read/unread (`/batch/read`, `/batch/unread`) or completely delete them (`/batch`) simultaneously.
- **Data export:** Unpaginated `/export` endpoint for auditing user notification histories.

## 📧 Emails module

Transactional email engine for automated communication:

- **Brevo API integration:** Direct HTTP integration with Brevo (formerly Sendinblue) for reliable and scalable delivery of transactional emails without SMTP overhead.
- **Dynamic HTML templates:** Rich, responsive email templates specifically designed for key platform events: Account Creation (Welcome), Password Resets, Role Updates, Status Changes (Blocks/Bans), Account Deletion, and Public Ticket Alerts.
- **Embedded assets (CID):** Native injection of brand assets (like the Foundry logo) directly into the email payload using Content-ID (CID), bypassing external image blocking in strict email clients (like Outlook) and guaranteeing immediate visual rendering.

## 📄 License

Property of **Antonio Corraliza León** as part of the Foundry development suite. All rights reserved.

