---
updatedAt: 2026-09-28T08:47:14.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Directory Structure

When you run `minikit-cli create my-app`, the generated codebase follows this structure:

```Plain
my-app/
├── .husky/                        # Git hooks
├── public/                        # Static assets
│   ├── index.html                 # HTML entry point
│   └── assets/
│       ├── icons/                 # Icon assets
│       └── illustrations/         # Image assets
│
├── src/                           # Source code
│   ├── main.tsx                   # React app entry point
│   ├── globals.d.ts               # Global type definitions
│   ├── vite-env.d.ts              # Vite environment types
│   ├── styles.css                 # Global styles
│
│   ├── bridge/                    # JSBridge handlers
│   │   ├── index.ts               # Bridge exports
│   │   ├── types.ts               # Bridge type definitions
│   │   ├── core.ts                # Core bridge logic
│   │   ├── cache.ts               # Bridge cache management
│   │   ├── handlers/              # Bridge handlers
│   │   │   ├── index.ts           # Export all handlers
│   │   │   └── device.ts          # Device info methods
│   │   └── __tests__/             # Bridge tests
│   │       ├── core.test.ts
│   │       └── cache.test.ts
│
│   ├── components/                # Reusable React components
│   │   ├── navbar.tsx             # Navigation bar
│   │   └── error-boundary.tsx     # Error boundary
│
│   ├── context/                   # React context providers
│   │   └── tanstack-query.tsx     # TanStack Query setup
│
│   ├── pages/                     # Page components & routing
│   │   ├── routes.ts              # Route definitions
│   │   ├── layout.tsx             # Root layout
│   │   ├── home.tsx               # Home page
│   │   ├── example.tsx            # Example page
│   │   └── example.test.tsx       # Page tests
│
│   ├── utils/                     # Utility functions
│   │   ├── app-name.ts            # App naming utils
│   │   ├── sanitise-html.ts       # HTML sanitization
│   │   └── test-utils.tsx         # Testing utilities
│
│   ├── hooks/                     # Custom React hooks (optional)
│   │   └── useAuthCode.ts         # Auth code hook
│
│   ├── api/                       # API layer (optional)
│   │   └── fetch-user-data.ts     # User data fetching
│
│   ├── constants/                 # App constants (optional)
│   │   └── locale.ts              # Locale constants
│
│   ├── debug/                     # Debug utilities (optional)
│   │   └── vconsole.ts            # vConsole integration
│
│   └── snap-checkout/             # Snap Checkout integration (optional)
│       ├── index.ts               # Snap checkout exports
│       ├── types.ts               # Type definitions
│       ├── snap-checkout.tsx      # Main component
│       ├── use-fetch-request.ts   # Hook for fetching requests
│       ├── fetch-request.ts       # Fetch logic
│       └── components.tsx         # Additional components
│
├── messages/                      # i18n message files (optional)
├── project.inlang/                # i18n configuration (optional)
│
├── .env.example                   # Environment variables template
├── .env.test                      # Test environment variables
├── .gitignore                     # Git ignore rules
├── .minikit.json                  # MiniKit configuration
├── .npmrc                         # NPM configuration
├── .nvmrc                          # Node version (NVM)
├── .releaserc.json                # Semantic release config
├── biome.json                     # Code formatter & linter
├── commitlint.config.js           # Commit message validation
├── index.html                     # Main HTML file
├── package.json                   # Dependencies and scripts
├── pnpm-workspace.yaml            # Workspace configuration
├── svgo.config.js                 # SVG optimization config
├── tsconfig.json                  # TypeScript configuration
└── vite.config.ts                 # Vite build configuration
```

| **File/Directory** | **Required?** | **Purpose**                                              |
| :----------------- | :------------ | :------------------------------------------------------- |
| .minikit.json      | **YES**       | MiniKit project configuration. Do not modify or delete.  |
| package.json       | **YES**       | Project dependencies, scripts, and metadata.             |
| package-lock.json  | **YES**       | Locked versions of dependencies for reproducible builds. |
| tsconfig.json      | **YES**       | TypeScript compiler configuration.                       |
| vite.config.ts     | **YES**       | Vite build tool configuration.                           |
| biome.json         | **YES**       | Code formatter and linter configuration.                 |
| .releaserc.json    | Optional      | Semantic release configuration for versioning.           |
| .gitignore         | **YES**       | Specifies files to exclude from git.                     |
| .env.example       | Optional      | Template for environment variables (without secrets).    |
| .env               | Optional      | Local environment variables (not committed to git).      |
| /src/bridge        | **YES**       | JSBridge handlers for native MiniApp communication.      |
| /src/components    | **YES**       | Reusable React UI components.                            |
| /src/pages         | **YES**       | Page components and routing logic.                       |
| /src/context       | **YES**       | React Context providers for global state.                |
| /src/utils         | **YES**       | Utility functions and helper methods.                    |
| /src/styles        | Optional      | Shared CSS files and design tokens.                      |
| /public            | **YES**       | Static assets served as-is.                              |
| /public/assets     | Optional      | Organized static files (icons, images, etc.).            |
| /.husky            | Optional      | Git hooks for code quality validation.                   |

***

#