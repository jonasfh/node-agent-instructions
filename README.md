# Node.js Agent Instructions

## Purpose

This repository provides standardized development guidelines, architectural conventions, dependency management rules, and testing standards for Node.js projects across the ecosystem.

## Modular Sub-guidelines

- 🏗️ **[Architecture & Backend Design](file:///./ARCHITECTURE.md)**: Layered structure, environment configuration, async patterns, error handling, and graceful shutdown.
- 📦 **[Package & Dependency Management](file:///./DEPENDENCIES.md)**: `npm` conventions, `package-lock.json`, dependency minimization, module systems (ESM/CommonJS), and scripts.
- 🧪 **[Testing & Quality Assurance](file:///./TESTING.md)**: Node test runners, boundary mocking, deterministic async tests, and quality standards.
- 🎨 **[Code Style & Idioms](file:///./CODE_STYLE.md)**: Modern JavaScript conventions, error handling hierarchies, and structured logging.

## Using this Submodule in Consuming Projects

Add this repository as a git submodule in your project under `.agents/node-agent-instructions/`:

```bash
git submodule add https://github.com/jonasfh/node-agent-instructions.git .agents/node-agent-instructions
```

In the consuming project's `AGENTS.md`, link to the modular sub-guidelines in `.agents/node-agent-instructions/` alongside the common guidelines.
