# ⚡ Foundry CLI

The architecture orchestration engine and code generation tool for the Foundry suite.

[![npm version](https://img.shields.io/npm/v/@antoniocorraliza/foundry-cli?color=a3e635&style=for-the-badge&logo=npm)](#)
[![Node.js](https://img.shields.io/badge/Node.js-18+-339933?style=for-the-badge&logo=nodedotjs)](#)
[![License](https://img.shields.io/badge/License-Proprietary-0f172a?style=for-the-badge)](#license)

## 🌐 Overview

**Foundry CLI** is the command-line orchestration engine for the Foundry suite. Designed to initialize complex architectures within Angular workspaces and execute strict code generation, it standardizes development workflows, injects primary providers, and automatically constructs predefined folder topologies.

## 📦 Installation

Install the CLI globally via npm to make the `foundry` command available across your workspace:

```bash
npm install -g @antoniocorraliza/foundry-cli
```

Once installed, verify the CLI version and available options in your terminal:

```bash
foundry --help
```

## ⚙️ Key features & security

- **Anti-overwrite defense:** Instantly aborts generation sequences if the target artifact already exists on disk, preventing accidental code loss.

- **Path traversal protection:** Enforces security checks and aborts execution if relative paths attempt to escape the project workspace root.

- **Intelligent path resolution:** Supports unified paths (e.g., `shared/format-date`) or separated path and name patterns (e.g., `shared/utils formatDate`). A dot (`.`) can be used to target default global directories.

- **VS Code integration:** Automatically generates and installs a comprehensive suite of custom code snippets tailored for the Foundry architecture inside the `.vscode` directory.

- **Environment validation:** Enforces strict execution within an active Angular workspace root by verifying the existence of `angular.json` and the `src/app` directory.

## 🚀 Execution protocols

The CLI exposes three primary orchestrator commands:

### `foundry init`

Bootstraps the Foundry suite architecture and core providers:

- Constructs the strict enterprise folder topology (`core`, `shared`, `services`, `pages`, `dialogs`, etc.).

- Installs core suite packages ensuring zero external UI dependencies (`@antoniocorraliza/foundry-core`, `foundry-ui`, `foundry-utils`).

- Registers base design system tokens in `src/styles.scss`.

- Updates TypeScript compiler options in `tsconfig.json` to support `ESNext`.

- Orchestrates `app.config.ts` by injecting global interceptors (Loader, Auth Refresh, JWT, Prefix) and core security/error handlers.

### `foundry generate <type> <path> [name]`

Executes strict code generation supporting unified paths or separated path and name patterns for architectural artifacts (Alias: `foundry g`).

### `foundry snippets`

Generates and installs custom code snippets tailored for the Foundry architecture directly into the active workspace (Alias: `foundry sn`).

## 🏗️ Generation targets & aliases

The CLI supports the generation of the following architectural artifacts, each governed by an automated template specification:

- **`feature`** (`f`): Complete feature ecosystem bundle (Component, Store, Constants).

- **`component`** (`c`): Standalone Angular component.

- **`dialog`** (`d`): Interactive dialog window bundle.

- **`store`** (`str`): Minimalist reactive state store.

- **`service`** (`s`): API service provider.

- **`entity`** (`e`): Interactive interface and data factory generator.

- **`route`** (`r`): Standalone lazy-loaded route definition.

- **`guard`** (`gu`): Router guard.

- **`interceptor`** (`i`): HTTP interceptor.

- **`directive`** (`di`): Standalone structural or attribute directive.

- **`pipe`** (`p`): Standalone data transformation pipe.

- **`enum`** (`en`): Strict TypeScript enumeration.

- **`type`** (`t`): Custom TypeScript type alias.

- **`adapter`** (`ad`): Functional DTO mapping adapter.

- **`resolver`** (`res`): Functional router data resolver.

- **`validator`** (`v`): Custom reactive forms validator.

- **`util`** (`u`): Pure utility function.

## ⚖️ License

Property of **Antonio Corraliza León** as part of the Foundry development suite. All rights reserved.

```

```
