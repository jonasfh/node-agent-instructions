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

## End-to-End & Visual Regression Testing (Playwright)

- **Fast Local Feedback (< 5–10s)**:
  - Run visual and UI tests locally **only** when actively developing or modifying UI, styling (CSS), templates, or frontend logic. Never run visual suites for purely backend, API, or database changes.
  - Restrict local checks to headless Chromium and focused, essential viewport sizes (e.g., desktop 1280px and mobile 375px).
- **Pre-cached Browser Binaries**:
  - Pre-install and cache browser binaries and OS dependencies inside dev containers or build environments to avoid runtime download latency, network dependency, or flaky installations.
- **Focused Locator Snapshots & Tolerances**:
  - Prefer capturing specific component containers or modals (`expect(locator).toHaveScreenshot()`) over full-page screenshots to reduce fragility from unrelated page elements or dynamic timestamps.
  - Configure reasonable visual tolerance (e.g., `maxDiffPixelRatio: 0.02` or threshold) to accommodate minor subpixel antialiasing differences across operating systems.
  - Maintain a clear workflow to review and commit golden reference updates (`--update-snapshots`) when design changes are deliberate.
- **Isolated Component Fixtures**:
  - Prefer loading isolated, lightweight HTML/CSS/JS fixtures when testing UI component layout, eliminating dependencies on backend database provisioning or full application server initialization.
- **Comprehensive CI Verification**:
  - Delegate broader visual test matrixes (multiple browsers, extended screen sizes, interactive animations) to CI pipelines (e.g., GitHub Actions). Ensure failure artifacts (diff screenshots) are uploaded as workflow artifacts for immediate inspection.

