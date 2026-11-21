# Node.js Agent Instructions

## Purpose

This repository provides standardized development guidelines, architectural conventions, dependency management rules, and testing standards for Node.js and frontend-tooling projects across the ecosystem.

It builds upon the core standards and multi-agent roles defined in [common-agent-instructions](https://github.com/jonasfh/common-agent-instructions).

## Modular Sub-guidelines

- 🏗️ **[Architecture & Backend Design](file:///./ARCHITECTURE.md)**: Layered structure, environment configuration, async patterns, error handling, and graceful shutdown.
- 📦 **[Package & Dependency Management](file:///./DEPENDENCIES.md)**: `npm` conventions, `package-lock.json`, dependency minimization, module systems (ESM/CommonJS), and scripts.
- 🧪 **[Testing & Quality Assurance](file:///./TESTING.md)**: Node test runners, Playwright visual regression testing, boundary mocking, deterministic async tests, and quality standards.
- 🎨 **[Code Style & Idioms](file:///./CODE_STYLE.md)**: Modern JavaScript conventions, error handling hierarchies, and structured logging.

## Progressive Skills (`skills/`)
- `ui-visual-regression`: Selective execution of `npm run test:js`, `npm run test:ui:fast`, and `npm run test:ui:update` for Frontend **Implementers** and **Verifiers**.

## Using this Submodule in Consuming Projects

Add this repository as a git submodule in your project under `.agents/node-agent-instructions/`:

```bash
git submodule add https://github.com/jonasfh/node-agent-instructions.git .agents/node-agent-instructions
```

In the consuming project's `AGENTS.md`, link to these modular sub-guidelines alongside `.agents/common-agent-instructions/`, and register `node-agent-instructions/skills` in `.agents/skills.json`.
