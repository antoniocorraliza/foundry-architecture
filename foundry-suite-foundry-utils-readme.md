# 🧰 Foundry utils

A framework-agnostic TypeScript utility library designed as the data processing core for the Foundry suite.

[![npm version](https://img.shields.io/npm/v/@antoniocorraliza/foundry-utils?color=a3e635&style=for-the-badge&logo=npm)](https://www.npmjs.com/package/@antoniocorraliza/foundry-utils)
[![TypeScript](https://img.shields.io/badge/TypeScript-Ready-3178C6?style=for-the-badge&logo=typescript)](#)
[![License](https://img.shields.io/badge/License-Proprietary-0f172a?style=for-the-badge)](#license)
[![Zero dependency](https://img.shields.io/badge/Dependencies-0-06b6d4?style=for-the-badge)](#)

## 🌐 Overview

**Foundry utils** is a pure logic library designed as the data processing and validation core for the Foundry suite. Built with zero external dependencies (excluding `tslib`), it provides stateless utility modules optimized for bundle size, security, and runtime predictability.

## ⚙️ Key features & design philosophy

- **Zero dependencies:** Completely self-contained to minimize bundle impact and eliminate external supply-chain vulnerabilities.

- **Full agnosticism:** Operates entirely independently of browser-specific DOM APIs or UI frameworks.

- **Functional purity:** Relies primarily on stateless pure functions, ensuring execution predictability and simplified testing.

- **Explicit naming:** Avoids cryptic abbreviations in favor of self-documenting, readable code structures.

## 📦 Installation

Install the package via npm:

```bash
npm install @antoniocorraliza/foundry-utils
```

## 🧩 Architecture & ecosystem

The library is organized into static function modules categorized by operational domain:

- **`FoundryApiNormalizationUtils`:** Handles bidirectional data transformation between backend `snake_case` keys (`\_id`) and frontend `camelCase` models.

- **`FoundryCommonUtils`:** Primitives for unique ID generation, secure UUID v4 creation, random alphanumeric codes, and asynchronous execution delays (`sleep`).

- **`FoundryCryptUtils`:** Lightweight data obfuscation using character-by-character hexadecimal encoding and decoding.

- **`FoundryCsvUtils`:** Automated browser CSV export with custom column mappings and asynchronous parsing into structured JSON.

- **`FoundryDateUtils`:** Temporal logic engine supporting interval calculations, calendar grid generation (`getDaysBy`), ISO week tracking, and multi-format parsing (`EU`, `JAP`, `PHP`).

- **`FoundryDebounceUtils`:** Execution timing controls providing global simple debouncers and independent form input tracking via isolated dictionaries (`formDebouncer`).

- **`FoundryFormatUtils`:** Formatters for currency, URL slugs, text truncation, string capitalization, and boolean normalization.

- **`FoundryFormDataUtils`:** Payload factory converting complex object graphs into multipart `FormData` combining text fields and binary streams.

- **`FoundryHashUtils`:** Cryptographic hash generators executing asynchronous `sha256` and `sha512` signatures via the native Web Crypto API (`crypto.subtle`).

- **`FoundryObjectUtils`:** Deep manipulation engine supporting immutable structural cloning (`cloneObject`), deep cleaning modes, and property difference detection (`getObjectDifferences`).

- **`FoundryValidationUtils`:** Mathematical and regular expression verifications including Spanish DNI/NIE modulus validation, email formats, URL structures, and password strength checks.

## 💻 Integration examples

For advanced use cases and fully developed code integration examples, visit the official documentation portal:

**🌐 [https://foundry-sandbox.vercel.app/foundry-utils](https://foundry-sandbox.vercel.app/foundry-utils)**

## 🛡️ Environment compatibility

Completely framework-agnostic, Foundry utils requires no specific version of Angular and integrates seamlessly into any modern TypeScript or JavaScript runtime (Node.js, React, Vue, Angular, or Vanilla JS).

## 📄 License

Property of **Antonio Corraliza León** as part of the Foundry development suite. All rights reserved.

