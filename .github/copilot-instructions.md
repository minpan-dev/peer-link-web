# Copilot instructions — peer-link-web

This file helps future Copilot sessions understand how to build, run, and reason about this repository.

---

## 1) Build, test, and lint commands

- Development (dev server + HMR):
  - npm run dev
- Production build (type-check + build):
  - npm run build
    - Note: this runs `tsc -b` first (project build / type-check) then `vite build`.
- Preview production build locally:
  - npm run preview
- Linting:
  - npm run lint

Tests:
- There are no test scripts or test runner configured in package.json currently.
- If tests are added later, single-test invocation depends on the chosen runner. Example patterns:
  - Vitest: npx vitest -t "test name" or npm run test -- -t "test name"
  - Jest: npx jest -t "test name" or npm run test -- -t "test name"


## 2) High-level architecture (big picture)

- Framework: React + TypeScript using Vite as the dev server and bundler (entry: index.html).
- Entry points:
  - src/main.tsx — app bootstrap (createRoot) and top-level render
  - src/App.tsx — root React component (currently scaffold/example content)
- Build flow:
  - TypeScript project build (`tsc -b`) is run before `vite build` to ensure project-level type checking and references are up-to-date.
- Styling and assets:
  - CSS lives under src (index.css, App.css) and assets are in src/assets.
  - public/ contains static assets referenced at runtime (e.g., icons.svg used via /icons.svg).
- Key libraries (from package.json):
  - @mui/material, @emotion/*: UI components and styling
  - zustand: lightweight state management (global store pattern expected)
  - livekit-client: real-time media client (project likely integrates or plans to integrate RTC features)
- Tooling:
  - ESLint is configured (eslint.config.js + dependencies) and the README mentions Oxc/ts-eslint configurations for stricter, type-aware linting.
  - Vite + @vitejs/plugin-react in vite.config.ts for React fast refresh and build.
- TypeScript configuration:
  - tsconfig.json + tsconfig.app.json and tsconfig.node.json exist to separate app and Node/tooling configs. The project uses `tsc -b` which implies project references or multi-config build.


## 3) Key conventions and patterns specific to this repo

- TypeScript-first: code is in .ts/.tsx. Build uses tsc before vite build to enforce type checking at project scope.
- Vite public assets: reference icons or SVGs under public/ via absolute paths (e.g., `/icons.svg#id`). Do not assume assets under src/assets are served from root — public/ is for static root-level references.
- Store and realtime libs present:
  - Zustand is included for app state; expect global store files (convention: src/store or src/stores). Search the repo for `create` from 'zustand' to find patterns.
  - livekit-client is present — components interacting with it will likely live under a features/rtc or components/rtc directory.
- ESLint and type-aware rules: README suggests using tseslint configs that require tsconfig paths (`tsconfig.app.json`, `tsconfig.node.json`). When adding stricter linting, update parserOptions.project to include these files.
- Scripts are minimal and conventional. Avoid adding build-time side-effects to `npm run dev` — keep type-only build in `npm run build`.


## 4) AI assistant / other assistant config files checked

Searched for and considered incorporating existing assistant rules/configs. None of the following files were found in the repository root:
- CLAUDE.md, AGENTS.md, .cursorrules, .cursor/, .windsurfrules, CONVENTIONS.md, AIDER_CONVENTIONS.md, .clinerules

If such files are added later, add short guidance here summarizing any repo-specific rules they contain.


## 5) Useful quick references for Copilot sessions

- Where to start:
  - Open src/main.tsx to see bootstrapping, then src/App.tsx for the root component.
  - Check package.json scripts for runnable commands.
- Common places to edit or inspect:
  - vite.config.ts — plugin and build-time transforms
  - eslint.config.js — lint rules and language options
  - tsconfig.app.json / tsconfig.node.json — type-aware settings used by ESLint or tsc


---

If you want, Copilot sessions can also add optional checks or scaffolding to this file (for example: recommended test runner + example scripts, Playwright/Playwright config, or CI snippets). Would you like to configure any MCP servers for this project (for example Playwright for end-to-end browser testing)?

(End of copilot-instructions.md)
