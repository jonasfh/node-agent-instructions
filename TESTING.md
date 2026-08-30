# Node.js Testing & Quality Assurance Guidelines

## Test Framework & Organization

- **Test Runners**:
  - Prefer the built-in Node.js test runner (`node:test` and `node:assert`) for lightweight, zero-dependency testing.
  - Alternatively, use established test runners like Vitest or Jest when advanced snapshotting or complex plugin ecosystems are needed.
- **Directory Layout**:
  - Colocate tests in a dedicated `test/` directory mirroring the `src/` hierarchy, or place `*.test.js` / `*.spec.js` next to their corresponding source modules.
- **Test Categorization**:
  - Distinguish unit tests (testing single functions or classes in isolation) from integration/end-to-end tests (testing multi-service interaction or HTTP workflows).

## Mocking & Boundary Isolation

- **External Boundary Mocking**: Mock only external boundaries (HTTP requests, SMS gateways, payment providers, third-party APIs). Avoid mocking internal business logic.
- **In-Memory Fakes**: Prefer realistic in-memory test doubles (e.g., fake SMS provider, fake database repository) over fragile method monkey-patching.
- **Native fetch Mocking**: Use mock interceptors (e.g., `undici.MockAgent` or custom fake servers) when testing HTTP interactions.

## Deterministic Testing Practices

- **State Isolation**: Clean up and reset shared state, in-memory caches, and database fixtures in `beforeEach` and `afterEach` hooks.
- **No Arbitrary Sleep Timers**: Do not use arbitrary delays (`setTimeout` / `sleep`) to wait for asynchronous operations. Use explicit Promises, event listeners, or condition polling with timeouts.
- **Port Allocation in HTTP Tests**: In HTTP integration tests, let the operating system allocate ephemeral ports by binding to port `0` (e.g., `server.listen(0)`), avoiding port conflicts across test runs.

## Code Quality & Static Analysis

- **Zero Lint Policy**: Enforce zero warnings and zero errors from linters (e.g., ESLint).
- **Automated Verification**: Run tests and linters in pre-commit checks and CI pipelines.
