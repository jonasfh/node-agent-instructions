# Node.js Architecture & Backend Design Standards

## Layered Architecture & Separation of Concerns

Structure Node.js applications into clear, decoupled layers:

1. **Transport / Entrypoint Layer**:
   - HTTP route handlers, controllers, CLI command entrypoints, and event listeners.
   - Responsible for parsing requests, validating input parameters, invoking domain services, and serializing responses.
   - Keep controllers thin; do not embed business rules or direct database queries in route handlers.

2. **Domain & Business Logic Layer**:
   - Pure business operations, workflows, calculations, and domain entity validations.
   - Independent of transport mechanisms (HTTP, CLI, WebSockets) and external providers.

3. **Data Access & Integration Layer**:
   - Database repositories, external HTTP API clients, and messaging queues.
   - Encapsulate third-party API interactions behind explicit client interfaces.

## Configuration & Environment Management

- **Process Environment**: Access runtime configuration exclusively via `process.env`.
- **Validation on Startup**: Validate all required environment variables at application startup (fail-fast principle) before listening on network ports.
- **No Hardcoded Secrets**: Never commit or hardcode credentials, connection strings, API tokens, or environment-specific URLs.
- **Safe Defaults**: Provide safe default values for local development where appropriate, ensuring non-production defaults cannot inadvertently connect to production services.

## Asynchronous Execution & Concurrency

- **Async/Await**: Exclusively use `async`/`await` and Promises for asynchronous operations. Avoid callback-based patterns and raw `.then()`/`.catch()` chains unless required by a specific third-party API.
- **Unhandled Rejections**: Ensure all asynchronous operations catch or propagate errors. Never leave unhandled promise rejections.
- **Controlled Concurrency**: Use `Promise.all` or `Promise.allSettled` when operations can run concurrently. Use bounded concurrency (e.g. batched iteration) when processing large datasets or making multiple outgoing API calls.

## Process Lifecycle & Graceful Shutdown

- **Signal Handling**: Implement handlers for `SIGINT` (Ctrl+C) and `SIGTERM` signals.
- **Resource Cleanup**: When shutting down:
  1. Stop accepting new incoming requests (`server.close()`).
  2. Wait for in-flight requests and background jobs to complete.
  3. Close database pools, socket connections, and clear any active timers (`setInterval`/`setTimeout`).
  4. Exit with code `0`.
- **Exit Discipline**: Never call `process.exit()` abruptly inside deep application logic or middleware; propagate errors to top-level handlers.
