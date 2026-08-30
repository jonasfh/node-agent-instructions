# Node.js Package & Dependency Standards

## Package Management with npm

- **Lockfiles**: Always commit `package-lock.json` and ensure it stays in sync with `package.json`.
- **Reproducible Installs**: Use `npm ci` (instead of `npm install`) in Docker builds and CI environments to ensure exact, reproducible dependency installations.
- **Dependency Classification**:
  - `dependencies`: Only packages strictly required to run the application in production.
  - `devDependencies`: Build tools, test runners, linters, formatters, and type declarations.

## Dependency Minimization

- **Node.js Built-ins First**: Leverage built-in Node.js standard library modules (`node:fs`, `node:path`, `node:http`, `node:crypto`, `node:test`, `node:util`, `node:events`, `node:stream`, `node:timers`) before introducing third-party packages.
- **Node Protocol Prefix**: Always use the `node:` prefix for Node.js standard library imports (e.g. `import fs from 'node:fs'` or `const path = require('node:path')`).
- **No Redundant Utilities**: Prefer modern JavaScript standard features (e.g., `Array.prototype.flat`, `Object.fromEntries`, native `fetch`, `structuredClone`) over legacy utility libraries like `lodash`, `underscore`, or `moment`.

## Module System Standards

- **ES Modules (ESM)**: Preferred for modern Node.js projects by setting `"type": "module"` in `package.json`.
- **Explicit Extensions in ESM**: When using ES Modules, always include file extensions in relative import specifiers (e.g., `import { helper } from './helper.js'`).
- **CommonJS Compatibility**: In repositories using CommonJS, consistently use `require` and `module.exports` without mixing module formats.

## Standard npm Scripts

Standardize script definitions across all Node.js projects:

- `npm start`: Runs the application in production mode.
- `npm run dev`: Starts the application with hot-reloading or development flags.
- `npm test`: Runs the automated test suite.
- `npm run test:watch`: Runs tests in watch mode during development.
- `npm run lint`: Runs linters (e.g., ESLint).
- `npm run format`: Formats code and documentation according to repository standards.
