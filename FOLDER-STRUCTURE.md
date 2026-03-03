## Project Folder Structure

This document describes the high-level folder structure for this Angular project and what each part is responsible for.

### Root

- **`src/`**: Application source code (Angular app, styles, assets).
- **`src/app/`**: Main Angular application code (root component, routing, core, shared, and feature areas).

### `src/app/core`

The **core layer** holds **single-instance, application-wide** functionality. Code here is not feature-specific and should generally be provided in the root injector.

- **`core/config/`**
  - Application-wide configuration, environment-aware settings, injection tokens, and global constants.
  - Examples: `APP_CONFIG` token, environment configuration, i18n/global date settings.

- **`core/guards/`**
  - Route guards that protect navigation or enforce access rules.
  - Examples: `AuthGuard`, `RoleGuard`, `UnsavedChangesGuard`.

- **`core/interceptors/`**
  - HTTP interceptors that apply to all HTTP calls (configured in the root provider list).
  - Examples: `AuthInterceptor` (adds JWT), `ErrorInterceptor`, `LoggingInterceptor`, `LanguageInterceptor`.

- **`core/services/`**
  - Singleton services that are shared across the entire app and are not tied to a single feature.
  - Examples: `AuthService`, `ApiClientService`, `LayoutService`, `NotificationService`.

- **`core/state/`**
  - Global application state management, if needed.
  - Examples: root-level store, global signal stores, configuration or user session state that many features depend on.

### `src/app/shared`

The **shared layer** holds **reusable building blocks** that can be used by multiple features but do not contain business-domain logic.

- **`shared/components/`**
  - Reusable UI components and widgets.
  - Examples: buttons, tables, cards, modals, form controls, pagination, generic layout components.

- **`shared/directives/`**
  - Attribute or structural directives that add cross-cutting behavior.
  - Examples: `debounceClick`, `hasPermission`, `autoFocus`, `scrollIntoView`.

- **`shared/pipes/`**
  - Pure or impure pipes for display formatting.
  - Examples: currency formatting, date formatting, translation, status labels.

- **`shared/models/`**
  - TypeScript interfaces, types, and models reused across multiple features.
  - Examples: `User`, `Pagination`, `ApiResponse<T>`, `SelectOption`.

- **`shared/utils/`**
  - Framework-agnostic utility helpers and pure functions.
  - Examples: date utilities, number helpers, mapping/adaptation helpers, validation helpers.

### `src/app/features`

The **features layer** is where application business domains live. Each folder under `features` represents a domain or module of the ERP (for example: `auth`, `dashboard`, `sales`, `inventory`, `settings`).

Common convention inside each feature:

- **`features/<feature>/pages/`**
  - Route-level containers (pages) loaded by the Angular router.
  - Examples: `login.page.ts`, `dashboard.page.ts`, `customer-list.page.ts`, `order-detail.page.ts`.

- **`features/<feature>/components/`**
  - UI components used only within that feature’s pages.
  - Examples: `customer-filter`, `order-items-table`, `kpi-card`, `sales-chart`.

- **`features/<feature>/data-access/`**
  - Data layer for the feature: API clients, repositories, adapters, and mappers.
  - Examples: `auth.api.ts`, `customer.repository.ts`, API DTO mapping utilities.

- **`features/<feature>/state/`**
  - Feature-specific state management (signals store, NgRx, component stores, etc.).
  - Examples: `auth.store.ts`, `dashboard.store.ts`, `sales.store.ts`.

- **`features/<feature>/*.routes.ts`**
  - Route definitions for the feature, usually lazy-loaded from the root `app.routes.ts`.

### Root App Files

Located directly under `src/app/`:

- **`app.ts`** and **`app.html`**
  - Root application component and its template. Typically includes the main layout shell and a `RouterOutlet`.

- **`app.routes.ts`**
  - Application-wide route configuration. Defines lazy-loaded routes for each feature and top-level routing structure.

- **`app.config.ts`** (and server variants)
  - Angular bootstrap configuration, global providers, HTTP interceptors, route reuse strategies, and any application-level setup.

