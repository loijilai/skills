# Topic Map

What a senior engineer is expected to own, across software engineering, backend, and infrastructure. Use it in step 2 to name the concepts a piece of work actually touches — especially the ones the user filed as plumbing.

An index, not a boundary or a curriculum. If the source touches something not listed, name that anyway.

## Software engineering

- **Layering and boundaries** — thin transport, fat service; what each layer may import; where transactions belong.
- **Coupling and cohesion** — what changes together, module seams, dependency direction.
- **Testing** — test levels chosen by seam; arrange–act–assert; failure paths; what a test that never fails costs you.
- **Refactoring** — code smells, behaviour-preserving change, working safely without tests.
- **Version control** — atomic commits, branching models, review as a design conversation.
- **Dependencies** — manifest vs lockfile, transitive drift, supply-chain risk.
- **12-Factor** — config in the environment, stateless processes, logs as streams.

## Backend

- **Concurrency** — race conditions, critical sections, why two workers break what one worker didn't.
- **Locking** — pessimistic vs optimistic, `SELECT … FOR UPDATE`, `SKIP LOCKED`, granularity, deadlock.
- **Transactions** — ACID, isolation levels and the anomalies each still permits, transaction boundaries vs business operations.
- **State machines** — legal transitions, guarded transitions, making illegal states unrepresentable.
- **Async work and queues** — broker / worker / result backend, producer–consumer, fan-out, why long work leaves the request cycle.
- **Delivery guarantees** — at-most-once, at-least-once, why exactly-once is a fiction; lease / visibility timeout / ACK.
- **Idempotency** — idempotency keys, deduplication, safe replay; at the job level and at the API boundary.
- **Retries** — transient vs permanent errors, exponential backoff with jitter, thundering herd, dead-letter queues.
- **Backpressure and rate limiting** — token buckets, queue depth as signal, shedding vs buffering.
- **API design** — resources and verbs, meaningful status codes, versioning, pagination, consistent error shapes.
- **Async API patterns** — `202` plus polling, webhooks, SSE, WebSocket, and which failure model favours each.
- **Trust boundaries** — server-side validation, read-only fields, mass assignment, parse don't validate.
- **Data modelling** — nullability as a claim, separate timestamps, normalisation and where to break it deliberately.
- **Query performance** — indexes and composite column order, query plans, N+1, eager loading, index cost on write.
- **Migrations** — DDL locks, expand / migrate / contract, zero-downtime with old and new code sharing a schema.
- **Engine differences** — concurrent write behaviour, lock granularity, feature support; dev/prod divergence.
- **Caching** — invalidation, TTL, stampede, read-through vs write-through, cache as a consistency decision.
- **Authentication and authorization** — who you are vs what you may do; OAuth 2.0 and OIDC; sessions vs tokens; PKCE; token lifetime and refresh.
- **Credential storage** — slow keyed hashes, per-user salt, work factor, timing-safe comparison.
- **Web vulnerability classes** — CSRF, XSS, SSRF, IDOR; structural defences rather than vigilance.
- **Secrets and least privilege** — injection vs secret manager, rotation, scoping a credential so a leak is bounded.

## Infrastructure and operations

- **Delivery pipelines** — build → test → package → deploy; build the artefact once and promote it.
- **Infrastructure as code** — declarative infrastructure, the server as a file in the repo, drift.
- **Immutable infrastructure** — replace rather than mutate; why manual ssh doesn't scale past one machine.
- **Environments** — parity, per-environment config and secrets, the divergences you can't avoid.
- **Deploy and rollback** — blue/green, canary, rolling; what a migration does to rollback; deploy decoupled from release via flags.
- **Containers and orchestration** — images and layers, resource limits, scheduling, health probes.
- **Failure models** — worker crash, broker restart, dropped connections, a third party that hangs rather than errors.
- **Resilience** — timeouts everywhere, retry vs fail fast, circuit breakers, partial failure as the normal case.
- **Durability** — what survives a restart, where state really lives, recovery on boot, backups you have actually restored.
- **Graceful shutdown** — SIGTERM, drain periods, in-flight work made resumable.
- **Observability** — logs, metrics, traces and the different questions each answers; structured logging, correlation ids, tracing across a queue.
- **Capacity** — connection pools, thread and worker sizing, load shedding, the difference between latency and throughput problems.
- **Networking** — DNS, TLS, load balancing, proxies, timeouts at every hop.

## Distributed systems

- **CAP and its trade-offs in practice** — what you actually give up during a partition.
- **Consistency models** — strong, eventual, read-your-writes; where each is acceptable.
- **Clocks and ordering** — why wall-clock time is not an ordering, logical clocks.
- **Consensus and coordination** — leader election, distributed locks and why they're harder than they look.
- **Data distribution** — replication, partitioning, hot keys, rebalancing.
- **Cross-service consistency** — sagas, outbox pattern, dual-write as a bug.
