# 🔎 Foundry arch scanner

An ultra-fast, static enterprise architecture analysis and governance engine for modern Angular applications.

[![npm version](https://img.shields.io/npm/v/@antoniocorraliza/foundry-arch-scanner?color=a3e635&style=for-the-badge&logo=npm)](https://www.npmjs.com/package/@antoniocorraliza/foundry-arch-scanner)
[![Node.js](https://img.shields.io/badge/Node.js-18+-339933?style=for-the-badge&logo=nodedotjs)](#)
[![Angular](https://img.shields.io/badge/Angular-19.2+-DD0031?style=for-the-badge&logo=angular)](#)
[![License](https://img.shields.io/badge/License-Proprietary-0f172a?style=for-the-badge)](#license)

## 🌐 Overview

**Foundry arch scanner** is an enterprise-grade static code analysis engine designed to enforce clean architecture, modern reactivity, strict memory management in RxJS, and prevent performance bottlenecks in Angular applications.

Built on top of `ts-morph`, it is highly optimized for CI/CD pipelines, providing ultra-fast, deep AST navigation and real-time generation of corporate audit reports in multiple formats (JSON, CSV, SARIF 2.1.0).

## 🏗️ Key features & architecture design

- **AST bnavigation & performance:** Leverages intelligent `WeakMap`-based caching and `Proxy` pattern acceleration to ensure amortized O(1) performance without V8 heap leaks, enabling lightning-fast scans even in massive enterprise monorepos.

- **Zero-CFG Pragmatism:** Employs a hybrid approach combining local AST navigation and 1-hop type resolution, bypassing heavy Control Flow Graphs (CFG). This strikes the perfect balance between high-speed CI/CD execution and deep diagnostic capabilities.

- **Enterprise quality gates:** Features a sophisticated statistical scoring engine (`ScoringEngine`) with configurable criticality thresholds capable of automatically blocking pipelines (`process.exit(1)`) upon architectural non-compliance.

- **Multi-format reporting:** Natively generates structured corporate reports in **SARIF 2.1.0**, **JSON**, and **CSV** for comprehensive auditing and analytics.

## 🔬 Core analysis domains & rules

The scanner evaluates codebases across four specialized analytical blocks:

### 1. RxJS & Memory Management

- **Infinite stream leak detection:** Audits safe completion operators (e.g., `takeUntilDestroyed`) to prevent memory leaks in infinite observables.

- **Subject lifecycle governance:** Detects uncompleted Subjects in root services that can persist eternally.

- **Eternal context exclusion:** Intelligently bypasses long-lived contexts (like `AppComponent`) where subscriptions do not require teardown.

### 2. Clean architecture & coupling

- **Standalone governance:** Enforces structural limits (`maxDependencies`, `maxComponentLines`, `maxStandaloneImports`) to prevent monolithic "God Components".

- **Domain isolation:** Detects domain leaks and unauthorized logic crossing boundaries.

- **Strict singleton encapsulation:** Enforces the `ServiceSignalEncapsulationRule`, requiring public mutable state in global root services to be exposed safely via `.asReadonly()`.
- **SSR Safety:** Validates Server-Side Rendering compliance (`HydrationSafetyRule`) by blocking unauthorized access to native browser globals.

### 3. Angular signals & modern reactivity

- **Computed purity strictness:** Validates absolute purity within `computed()`, flagging any side effects or mutations.

- **Effect infinite loop prevention:** Statically detects circular dependency loops inside `effect()` blocks.

- **Zone mixing detection:** Flags legacy manual change detection triggers (`detectChanges`, `markForCheck`) in modernized reactive zones.

- **Migration suggestions:** Identifies legacy patterns and suggests modern primitive upgrades (`toSignal`, `resource`, `linkedSignal`).

### 4. Optimization & performance

- **Change detection strategy audit:** Enforces `MissingOnPushRule` to ensure UI components are not eagerly re-rendered.

- **Event listener frequency:** Audits high-frequency DOM events bound via `@HostListener` that trigger excessive change detection cycles.

- **Heavy initialization:** Flags expensive synchronous operations within class property initializers.

## 📊 Architecture scoring engine & quality gates

The **Foundry arch scanner** engine goes beyond simple vulnerability detection; it implements a statistical and deterministic model designed to quantify technical debt and evaluate the structural health of Angular applications. This approach allows Enterprise teams to establish strict, automated, and measurable **quality gates** in their continuous integration (CI/CD) cycles.

The internal mechanics of the _scoring engine_ for calculating architectural metrics are detailed below.

### 1. Violation severity weighting

Each violation detected in the source code is classified and penalized based on its direct impact on system stability, performance, or maintainability.

| Severity     | Weight (Points) | Architectural Criterion                                                                                                        |
| ------------ | --------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| **CRITICAL** | $10$            | Severe violations (e.g., memory leaks, uncontrolled state mutations, circular dependencies). Potential system blockage.        |
| **WARNING**  | $3$             | Anti-patterns and excessive coupling. They don't break the app immediately but generate significant short-term technical debt. |
| **INFO**     | $1$             | Refactoring opportunities and minor deviations from code conventions (e.g., missing use of modern primitives).                 |

### 2. Defect density calculation

To ensure fair evaluations regardless of repository size, the engine calculates a **defect density** for each analytical block.

To prevent a single error from disproportionately penalizing isolated components or very small projects, the engine implements a smoothing threshold (`SMALL_PROJECT_SMOOTHING_THRESHOLD = 15`). This ensures that the minimum divisor of evaluated files is always $15$.

$$
\text{Defect density} = \frac{\sum \text{Weights}}{\max(\text{Scanned files}, 15)}
$$

### 3. Block score formula

Each analytical block starts from a base score of 100 perfect points. A penalty proportional to the defect density multiplied by a strict severity factor (`DENSITY_PENALTY_MULTIPLIER = 15`) is applied. The final value is rounded and floored to avoid negative scores.

$$
\text{Block score} = \max\left(0, \text{round}\left(100 - (\text{Defect density} \times 15)\right)\right)
$$

### 4. Grade assignment

The obtained numeric score is translated into a standardized letter grade, providing an immediate reading of the project's risk level:

- **A (**$\ge 90$ **points):** Excellent architectural compliance. Clean, reactive, and highly optimized code.

- **B (**$\ge 80$ **points):** Good structural condition with minor observations.

- **C (**$\ge 70$ **points):** Moderate warnings. Technical debt detected that should be scheduled for refactoring.

- **D (**$\ge 60$ **points):** Significant architectural risk. Strongly discouraged practices present in the code.

- **F (**$< 60$ **points):** Critical non-compliance. Project integrity is compromised.

### 5. Overall project score

The overall state of the application is determined by the strict arithmetic mean of the scores obtained in the four analysis domains:

1. RxJS & Memory management

2. Clean architecture & Coupling

3. Angular signals & Modern reactivity

4. Optimization & Performance

$$
\text{Overall score} = \frac{\text{Score}_{\text{RxJS}} + \text{Score}_{\text{Arch}} + \text{Score}_{\text{Signals}} + \text{Score}_{\text{Perf}}}{4}
$$

### 🛑 CI/CD Pipeline & Quality Gate Impact

The _scorign engine_ is designed to act as an automated guardian in DevSecOps environments. The engine will automatically block the pipeline (via `process.exit(1)`) if any of the following _quality gate_ failure conditions are met:

- **Critical grade:** The overall project score drops below 60 points (Grade **F**).

- **Critical overflow:** The total number of issues categorized as `CRITICAL` exceeds the maximum limit configured in `foundry-arch-scanner.json` (`maxCriticalIssues`).

- **Warning overflow:** (Optional) If a limit for `maxWarnings` is defined and exceeded.

> **💡 CI/CD tip:** During early adoption phases or legacy code migrations, you can run the scanner with the `--warn-only` flag to generate full analytical reports without interrupting the deployment.

## 🚀 Installation & usage

The `foundry-arch-scanner` is distributed via NPM and can be executed directly or installed globally/locally within your Angular workspace.

### Direct execution (npx)

Execute the scanner directly against your Angular project path without prior installation:

```bash
npx @antoniocorraliza/foundry-arch-scanner ./src/app
```

### Global installation

Install the scanner globally for system-wide availability:

```bash
npm install -g @antoniocorraliza/foundry-arch-scanner
foundry-arch-scanner ./src/app
```

### Local workspace installation (Dev dependency)

Install the scanner as a development dependency for CI/CD pipeline integration:

```bash
npm install -D @antoniocorraliza/foundry-arch-scanner
npx foundry-arch-scanner ./src/app
```

### CI/CD pipeline flags

Use the `--warn-only` flag to generate reports and calculate scores without intentionally blocking the pipeline (bypasses `process.exit(1)` on failure).

```bash
npx foundry-arch-scanner ./src/app --warn-only
```

## ⚙️ Configuration

The engine relies on a centralized governance file (`foundry-arch-scanner.json`) located at the root of your Angular workspace. This file dictates the strict architectural thresholds, boundary rules, and CI/CD quality gates under which the application is audited.

If the file is not present, the engine will fallback to its internal default enterprise thresholds.

### Configuration File (`foundry-arch-scanner.json`)

```json
{
  "architecture": {
    "uiComponentPaths": ["src/app/shared/components/"],
    "maxDependencies": 20,
    "maxComponentLines": 500,
    "allowedUiServices": [
      "FoundryRouterService",
      "FoundryDialogWindowService",
      "NetworkStatusService",
      "ThemeService",
      "TranslationService",
      "IconRegistryService",
      "I18nService"
    ],
    "domainRoots": [],
    "forbiddenGlobals": [
      "window",
      "document",
      "localStorage",
      "sessionStorage"
    ],
    "dataLayerSuffixes": ["Repository", "DataService", "ApiClient"],
    "serviceSuffixes": ["Service", "Store", "Facade", "Repository"]
  },
  "qualityGate": {
    "maxCriticalIssues": 0,
    "minOverallScore": 90
  }
}
```

### Governance parameters breakdown

The configuration schema is divided into two primary domains: **Architecture** and the **Quality gate**.

- **`architecture.uiComponentPaths`**: Target directories monitored for strict UI component governance. Components inside these paths are heavily audited to ensure they implement `ChangeDetectionStrategy.OnPush` and do not contain leaked domain logic.

- **`architecture.maxDependencies` & `architecture.maxComponentLines`**: Coupling thresholds and maximum size constraints designed to prevent the emergence of monolithic "God Components". Exceeding these limits triggers coupling warnings.

- **`architecture.allowedUiServices`**: An explicit whitelist of acceptable services that can be injected into presentation layers or UI components. Any attempt to inject unauthorized services (e.g., business logic or HTTP repositories) will be flagged as a boundary leak.

- **`architecture.forbiddenGlobals`**: Strict prohibition of native browser global objects. Accessing these globals directly without Angular's `DOCUMENT` token or `isPlatformBrowser` guards will result in a critical violation to guarantee strict Server-Side Rendering (SSR) safety and prevent memory leaks.

- **`architecture.dataLayerSuffixes` & `architecture.serviceSuffixes`**: Naming conventions utilized by the AST engine to identify, isolate, and audit data layers, state stores, and singleton services (e.g., verifying that a `*Repository` does not manually subscribe to an observable).

- **`qualityGate.maxCriticalIssues` & `qualityGate.minOverallScore`**: Execution thresholds that dictate the CI/CD pipeline blocking behavior. If the global audit grade drops below the defined minimum score (`minOverallScore`), or if the total number of critical issues exceeds `maxCriticalIssues`, the scanner will intentionally halt the pipeline with `process.exit(1)`.

## 🤫 Developer suppression layer

In scenarios where an architectural exception is necessary, developers can selectively suppress rules using inline control comments.

Suppress a rule on the same line:

```ts
// arch-scanner-disable architecture-direct-dom-manipulation
const element = this.el.nativeElement;
```

Suppress a rule on the next line:

```ts
// arch-scanner-disable-next-line rxjs-memory-leak
this.infiniteStream$.subscribe();
```

## 📦 Peer dependencies

This suite is built on top of the latest Angular features and Node environments. Make sure your environment satisfies the following:

| PACKAGE        | REQ. VERSION     | PURPOSE IN THE SUITE                                     |
| :------------- | :--------------- | :------------------------------------------------------- |
| **Node.js**    | `v18.13+ / v20+` | Compatible with the LTS versions required by Angular 19. |
| **TypeScript** | `>=5.4.0`        | Required for AST compilation and parsing.                |
| **Angular**    | `>=19.0.0`       | Required for modern reactivity and signals architecture. |

## ⚖️ License

Property of **Antonio Corraliza León** as part of the Foundry development suite. All rights reserved.
