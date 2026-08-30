# Node.js Code Style & Idioms

## JavaScript & TypeScript Standards

- **Variable Declarations**: Always use `const` by default. Use `let` only when variable reassignment is strictly required. Never use `var`.
- **Strict Equality**: Always use `===` and `!==`. Never use loose equality operators (`==` or `!=`).
- **Modern Language Features**: Use modern ECMAScript idioms:
  - Destructuring assignments for objects and arrays.
  - Template literals for string formatting instead of string concatenation.
  - Optional chaining (`?.`) and nullish coalescing (`??`) for defensive property access and default values.
  - Arrow functions for concise callbacks and preserving lexical `this`.

## Error Handling & Exceptions

- **Error Objects**: Always throw instances of standard `Error` or custom subclasses extending `Error` (e.g. `class ValidationError extends Error`). Never throw strings, numbers, or plain literal objects.
- **Error Context**: Preserve original error stack traces when wrapping errors, using the `cause` option where supported: `new Error('Failed to process message', { cause: err })`.
- **Async Error Boundaries**: Ensure all Promise chains and `async` functions handle rejections or let them bubble up to unified error-handling middleware.

## Logging Practices

- **Structured Logging**: Use JSON-formatted structured logging for application output in server environments.
- **Log Levels**: Use appropriate levels:
  - `error`: Unhandled exceptions, failed critical operations, data corruption.
  - `warn`: Recoverable anomalies, fallback paths taken, deprecated API usage.
  - `info`: Key lifecycle events (server started, configuration loaded, major job completed).
  - `debug`: Detailed diagnostics useful during development or troubleshooting.
- **Security & Privacy**: Never log sensitive user credentials, access tokens, API keys, passwords, or Personally Identifiable Information (PII).
