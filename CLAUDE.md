# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Build & Run Commands

```bash
npm install          # Install dependencies
npm run build        # TypeScript compile + chmod executable
npm start            # Run the MCP server
```

There are no tests or lint commands configured in this project.

## Architecture Overview

This is an MCP (Model Context Protocol) server that wraps Apple's App Store Connect API. The server exposes 20+ tools for managing apps, beta testing, bundle IDs, devices, users, analytics, and localizations.

### Core Components

**Entry Point** (`src/index.ts`):
- `AppStoreConnectServer` class orchestrates everything
- Loads env config, instantiates handlers, builds tool list, dispatches requests
- Tools conditionally registered (sales/finance require `VENDOR_NUMBER`)

**Service Layer** (`src/services/`):
- `AppStoreConnectClient` - Axios HTTP client for Apple API (`/v1` endpoints)
- `AuthService` - JWT generation using ES256 with .p8 private key (20-min expiry)

**Handler Pattern** (`src/handlers/`):
8 handler classes, each receiving `AppStoreConnectClient` via constructor:
- `AppHandlers` - App listing/info
- `BetaHandlers` - Groups, testers, feedback screenshots
- `BundleHandlers` - Bundle IDs and capabilities
- `DeviceHandlers` - Device management
- `UserHandlers` - Team members
- `AnalyticsHandlers` - Reports, sales, finance
- `LocalizationHandlers` - App versions and localizations
- `XcodeHandlers` - Scheme listing via `xcodebuild -list`

**Type System** (`src/types/`):
JSON:API format interfaces with `id`, `type`, `attributes`, `relationships`. One file per domain (apps.ts, beta.ts, bundles.ts, etc.).

**Utilities** (`src/utils/validation.ts`):
- `validateRequired()` / `validateEnum()` - Input validation
- `sanitizeLimit()` - Pagination (1-200, default 100)
- `buildFilterParams()` / `buildFieldParams()` - API query building

### Data Flow

```
Tool Call → index.ts dispatch → Handler method → Client.get/post → AuthService.generateToken → Apple API
```

### Adding a New Tool

1. Add handler method in appropriate `src/handlers/*Handlers.ts`
2. Add TypeScript types in `src/types/*.ts`
3. Register tool schema in `buildToolsList()` in `index.ts`
4. Add case in `CallToolRequestSchema` switch statement

## Environment Variables

Required:
- `APP_STORE_CONNECT_KEY_ID` - API Key ID
- `APP_STORE_CONNECT_ISSUER_ID` - Issuer ID
- `APP_STORE_CONNECT_P8_PATH` - Path to .p8 private key file

Optional:
- `APP_STORE_CONNECT_VENDOR_NUMBER` - Enables sales/finance report tools
