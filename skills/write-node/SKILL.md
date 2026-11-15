---
name: write-node
description: "Develop and debug Node.js applications and TypeScript runtime code. Use for native type stripping, async behavior, streams, caching, errors, shutdown, tests, profiling, modules, logging, or environment configuration."
---

# write-node

## Goal

Produce reliable Node.js code with explicit runtime, resource, and failure behavior.

## Scope

- Apply to requested Node.js implementation or diagnosis. Respect the project's installed runtime, package manager, libraries, module system, and test conventions.
- Use relevant branches below; a local change does not require a whole-stack audit or new dependencies.
- Native TypeScript execution does not replace type checking or justify changing an established build pipeline.

## Workflow

1. Read project instructions, package manifests, lockfile, runtime constraints, relevant source, and existing checks.
2. Inspect actual dependency versions and types before relying on API signatures. Resolve package entry points and pnpm symlinks rather than searching every installed package.
3. Reproduce the behavior or define the intended contract. Select the applicable guidance below and implement the smallest supported change.
4. Register cleanup where resources are created. Preserve error causes, cancellation, concurrency limits, and shutdown semantics.
5. Run affected type, behavior, and runtime checks. For performance claims, compare equivalent workloads and report measurements.

## Rules

### TypeScript and modules

- For native type stripping, verify support and required flags against the actual Node version. Use explicit `.ts` import extensions for source execution and `import type` for erased imports.
- Avoid syntax requiring transformation, including enums, runtime namespaces, constructor parameter properties, and unsupported decorators. Use const objects or ordinary properties where appropriate.
- Use `NodeNext` module/resolution settings and compatible options such as `noEmit`, `allowImportingTsExtensions`, and `verbatimModuleSyntax`; check compiler-version support before changing configuration.
- Run `tsc --noEmit` separately: runtime type stripping does not validate types.
- If publishing compiled JavaScript, verify emitted import extensions, declarations, package exports, and consumer compatibility. Keep source execution and distribution settings distinct.
- Prefer ESM and named exports for new code where compatible; preserve established CommonJS contracts. Native ESM requires explicit relative file extensions.
- Use supported JSON import attributes and `import.meta` path helpers for the installed runtime. Avoid adding barrels or module migrations without a concrete need.

### Async operations

- Prefer readable `async`/`await`. Use `Promise.all` for independent operations and `Promise.allSettled` when individual failures must be collected; inspect every outcome.
- Bound concurrency for large collections or limited resources, using existing utilities such as `p-limit` or `p-map` when installed.
- Await operations whose completion or failure matters. Use factories for asynchronous initialization.
- Use cancellation and timeouts for long-running work; clear timers and release resources in `finally`.

### Errors and logging

- Follow one coded-error strategy; preserve the original error through `cause`. Existing `@fastify/create-error` is suitable when used by the project.
- Narrow unknown errors before inspecting codes. Catch when recovery, boundary translation, or meaningful context is needed; otherwise propagate.
- Never swallow errors or leak internal details to clients. Log structured context at the responsible boundary, avoiding duplicate reports.
- Use existing structured logging, request IDs, child loggers, serializers, levels, and redaction. Pino is suitable where already installed.
- Keep credentials, tokens, and unnecessary personal data out of logs, commands, and reports.
- Fatal exceptions require bounded shutdown rather than continuing in unknown state. Integrate with the project's shutdown mechanism.

### Streams and ingestion

- Prefer awaited `pipeline` from `node:stream/promises` over unchecked chained `.pipe()` for completion, errors, and backpressure.
- For CSV, ETL, large files, and in-stream transformations, show an explicit `async function*` transform when useful. Keep buffering bounded and handle records spanning chunks.
- Use a real parser for quoted CSV; splitting chunks by comma/newline is insufficient. Preserve multibyte text across chunk boundaries.
- When writing manually, respect `write()` returning false and await `drain`, handling errors and cancellation.
- Stream consumers that collect text/JSON/buffers load the whole result; reserve them for bounded inputs.

```typescript
import { pipeline } from "node:stream/promises";
import { createReadStream, createWriteStream } from "node:fs";
import { createGzip } from "node:zlib";

await pipeline(
  createReadStream(input),
  createGzip(),
  createWriteStream(output),
);
```

### Caching

- Choose explicitly when repeated work is material: bounded `lru-cache` for process-local reuse, `async-cache-dedupe` for in-flight request deduplication or stale-while-revalidate when those libraries fit the project.
- Define key scope, maximum size, TTL and units, invalidation after mutation, and permitted staleness. Do not cache sensitive results without caller/tenant isolation.
- Use shared storage only when cross-instance consistency or reuse requires it. Check installed APIs before implementing invalidation.
- ETL enrichment can combine an async-generator transform with cached repeated lookups. Serial processing alone does not demonstrate concurrent deduplication.
- Avoid caches for data requiring immediate consistency or values that exhaust memory. Do not add caching merely because a prompt mentions ingestion.

### Shutdown and resources

- Handle SIGTERM/SIGINT through the existing mechanism; `close-with-grace` is an option where available.
- Mark readiness false, stop accepting new work, drain in-flight work, close dependent clients/pools, and exit with an appropriate status within the orchestrator deadline.
- Await actual closure APIs; some server APIs are callback-based. Verify framework signal handling rather than assuming close hooks install handlers.
- Make shutdown idempotent and bounded. Release resources even when another cleanup fails; respect dependency order.
- Track and clear timers, listeners, sockets, workers, child processes, watchers, readline interfaces, and database/cache clients.

### Tests, flakiness, and hangs

- Follow the existing runner; prefer `node:test` for compatible new projects. Use test-scoped mocks and deterministic setup/teardown.
- Register cleanup immediately after resource creation, for example with `t.after`. Await close/disconnect/terminate operations.
- Subscribe to events before triggering them. Wait on actual completion rather than arbitrary sleeps.
- Isolate state and fixtures; use dynamic ports (`0`), fixed time when relevant, and controlled external services. Register rollback/cleanup even when assertions fail.
- For hangs: isolate file then test name, add supported reporter/timeout options, capture active-handle ownership, fix teardown in the creating scope, then verify repeated isolated runs and the full suite.
- If already available, `why-is-node-running` with its supported preload and signal interface can identify remaining handles; keep diagnostic tooling/output scoped and temporary.
- For flakes, compare concurrency, timezone, clock, random seeds, shared state, CI resources, event ordering, and unawaited promises. Temporary retries can diagnose; they do not fix the root cause.

Example commands; verify options against the installed runner:

```sh
node --test --test-reporter=spec --test-timeout=15000 path/to/file.test.ts
node --test --test-name-pattern='closes resources' path/to/file.test.ts
node --test
```

### Performance and dependencies

- Reproduce under representative load; capture a CPU or memory profile before optimizing. Built-in `--cpu-prof`/`--heap-prof`, installed flame tools, or inspectors can provide evidence.
- Inspect event-loop blocking, serial work, stream backpressure, connection pooling, unbounded caches, listener leaks, and retained resources.
- Use bounded worker pools for demonstrated CPU bottlenecks and release pooled connections in `finally`.
- Benchmark with existing tooling such as autocannon, wrk, or k6 only in an authorized environment; report workload, concurrency, duration, latency, throughput, and error rate.
- For dependency questions, inspect the installed package manifest, exports, types, source, and peer dependencies; use the project's package-manager `why`/`list` equivalents. Do not infer actual versions from manifest ranges alone.

### Environment

- Use the project's environment-loading mechanism; supported Node versions offer `--env-file` and `process.loadEnvFile()`.
- Parse and validate configuration once at startup using the installed schema tools. Expose a typed configuration object with explicit defaults.
- Prefer separate flags for logging, rate limits, infrastructure, and features rather than coupling unrelated behavior to `NODE_ENV`; retain framework-required uses.
- Keep secrets out of version control and reports. Document keys with safe placeholders in requested example configuration; preserve existing local files.

## Verification

- Run relevant existing typecheck, test, lint, and runtime checks; verify feature flags/options against installed versions.
- For hangs/flakes, confirm repeatable isolated success, normal full-suite exit, and absence of unexpected handles. State CI status separately if not observed.
- For streams/caches, check bounded memory, errors, cancellation, invalidation, and tenant scope where relevant.
- For shutdown, verify actual resource closure and deadline handling; for optimization, compare equivalent before/after measurements.
- Do not claim checks or remote execution that were not performed.

## Output

Report implemented changes or diagnosis, supporting runtime/source evidence, check results, and remaining uncertainty. Include benchmark data or reproduction commands when relevant.
