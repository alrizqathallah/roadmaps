# Node.js Backend Development Learning Roadmap
### From Zero to Industry-Ready — Practical, Structured, Effective

---

## How to Use This Roadmap

This roadmap is divided into **5 phases**. Each phase builds on the previous one and includes:
- **Core concepts** to learn
- **Exercises** (small, targeted drills)
- **Mini-projects** (1–3 day builds)
- **Large projects** (1–2 week builds)
- **Industry relevance notes** to keep you grounded in real-world expectations

Estimated total time: **10–16 months** at ~10–15 hours/week.

---

## Prerequisites

Before starting, you should be comfortable with:
- Basic JavaScript: variables, functions, arrays, objects, loops
- Using a terminal / command line
- A code editor (VS Code recommended)

If not, spend 3–4 weeks on JavaScript fundamentals first (see [javascript.info](https://javascript.info)).

---

## Phase 1 — Node.js & JavaScript Foundations
### Goal: Understand Node.js deeply, how it differs from browser JS, and how to write solid server-side JavaScript.

---

### 1.1 How Node.js Works

**Concepts:**
- What Node.js is: V8 engine + libuv + event loop
- The event loop in detail: call stack, task queue, microtask queue, phases
- Blocking vs. non-blocking I/O
- Single-threaded concurrency model
- Node.js vs. browser JavaScript: globals, modules, APIs
- The Node.js release cycle: LTS vs. Current — always use LTS in production

**Industry Note:** Most Node.js bugs in production stem from misunderstanding the event loop. Developers who grasp it debug async issues in minutes; others spend days.

**Exercises:**
1. Predict the console output order of a snippet mixing `setTimeout`, `Promise.resolve()`, and `process.nextTick`. Then verify — and explain why.
2. Write a function that deliberately blocks the event loop (e.g., a large `for` loop). Measure its impact on a concurrent HTTP server using `ab` or `autocannon`.
3. Rewrite the blocking function to be non-blocking using `setImmediate` and chunked processing.

---

### 1.2 Modern JavaScript for Backend

**Concepts:**
- ES Modules (`import`/`export`) vs. CommonJS (`require`/`module.exports`)
- Destructuring, spread/rest, optional chaining, nullish coalescing
- Promises: `.then`, `.catch`, `.finally`, `Promise.all`, `Promise.allSettled`, `Promise.race`
- `async`/`await` and error handling patterns
- Iterators, generators, and `for await...of`
- `WeakMap`, `WeakSet`, `Map`, `Set`
- Error types: `Error`, `TypeError`, `RangeError` — extending `Error`

**Industry Note:** Understanding `Promise.allSettled` vs. `Promise.all` is a frequent interview topic — and a real production concern when calling multiple external APIs.

**Exercises:**
1. Implement a `retry(fn, attempts, delay)` utility that retries a failing async function up to N times with a delay between attempts.
2. Write a `promisePool(tasks, concurrency)` function that runs async tasks with a maximum concurrency limit.
3. Use `for await...of` to read a large file line by line without loading it entirely into memory.

---

### 1.3 Node.js Core Modules

**Concepts:**
- `fs`: `readFile`, `writeFile`, `createReadStream`, `createWriteStream`, `watch`
- `path`: `join`, `resolve`, `dirname`, `extname`, `basename`
- `os`: system info, CPU and memory stats
- `events`: `EventEmitter` — `on`, `emit`, `once`, `off`, `removeAllListeners`
- `stream`: Readable, Writable, Transform, Duplex — pipe, backpressure
- `buffer`: binary data, encoding, conversion
- `crypto`: hashing, HMAC, random bytes, encryption basics
- `child_process`: `exec`, `spawn`, `fork`
- `worker_threads`: CPU-bound work off the main thread
- `http` / `https`: raw HTTP server creation

**Industry Note:** Streams are one of the most underused and most powerful Node.js primitives. Processing a 10GB file with streams uses 30MB of RAM; loading it in full crashes your server.

**Exercises:**
1. Build a CLI tool using only `fs` and `path` that recursively lists all `.js` files in a directory with their sizes.
2. Build a Transform stream that converts CSV input to JSON output — pipe a file through it.
3. Use `crypto` to implement a `hashPassword(password)` function using `scrypt` and a `verifyPassword(password, hash)` function.
4. Use `worker_threads` to offload a CPU-intensive Fibonacci computation and compare execution time vs. the main thread.

**Mini-Project: File Processing CLI**
- Accept a directory path as a CLI argument
- Recursively find all files matching a given extension
- For each file, count lines, words, and characters
- Stream results into a summary CSV report
- Handle errors gracefully (missing directory, permission denied)

---

### 1.4 TypeScript for Node.js

**Concepts:**
- TypeScript compiler (`tsc`), `tsconfig.json` for Node.js
- Types vs. interfaces, generics, utility types
- Typing async functions, Promises, and error handling
- Module augmentation and declaration merging
- `ts-node` and `tsx` for development
- Build pipeline: `tsc` + `esbuild` or `swc` for production

**Industry Note:** TypeScript is the default in professional Node.js projects. All large projects in this roadmap use it. Learn it now, not later.

**Exercises:**
1. Type a `paginate<T>(items: T[], page: number, limit: number): PaginatedResult<T>` generic utility.
2. Create a typed `Result<T, E>` type that represents either a success or failure — implement two functions using it.
3. Configure a strict `tsconfig.json` for Node.js and fix all errors it surfaces in an existing JS file.

---

## Phase 2 — HTTP, APIs & Databases
### Goal: Build production-quality REST APIs connected to real databases, with proper validation, error handling, and authentication.

---

### 2.1 HTTP Deep Dive

**Concepts:**
- HTTP/1.1 vs. HTTP/2: multiplexing, header compression, server push
- HTTP methods: GET, POST, PUT, PATCH, DELETE — correct semantics
- Status codes: 2xx, 3xx, 4xx, 5xx — when to use each
- Headers: `Content-Type`, `Authorization`, `Cache-Control`, `ETag`, `If-None-Match`
- CORS: preflight requests, `Access-Control-Allow-*` headers
- Cookies: `Set-Cookie`, `HttpOnly`, `Secure`, `SameSite`
- Request lifecycle: DNS → TCP → TLS → HTTP → response
- REST architectural constraints vs. REST in practice

**Industry Note:** A developer who understands HTTP at this level writes APIs that frontend teams don't constantly complain about — and can debug network issues without guessing.

**Exercises:**
1. Using only Node's `http` module (no framework), build a server that routes `GET /users` and `POST /users` and returns JSON.
2. Implement correct CORS handling manually. Test preflight requests with `curl`.
3. Implement `ETag`-based caching for a GET endpoint. Verify it returns `304 Not Modified` on the second request.

---

### 2.2 Express.js

**Concepts:**
- Application setup, middleware chain, request/response lifecycle
- Routing: `app.get`, `app.use`, `express.Router()`
- Middleware types: application-level, router-level, error-handling, third-party
- Request object: `params`, `query`, `body`, `headers`, `cookies`
- Response methods: `json`, `send`, `status`, `redirect`, `set`
- Error handling middleware: the 4-argument signature `(err, req, res, next)`
- Static file serving
- Popular middleware: `helmet`, `morgan`, `compression`, `cors`

**Industry Note:** Express is the most common Node.js framework in existing codebases. Even if your next job uses Fastify or NestJS, you'll likely maintain Express services.

**Exercises:**
1. Build a middleware that logs method, path, status, and response time for every request — in the format that real APM tools expect.
2. Implement a global error handler that distinguishes operational errors (user errors) from programmer errors (bugs) and responds appropriately.
3. Build a router-level middleware that rate-limits requests per IP using an in-memory Map (no library).

**Mini-Project: Notes REST API**
- CRUD for notes (`/notes` resource)
- In-memory storage (Map or array) — no database yet
- Request body validation (manual or with `joi`)
- Proper HTTP status codes
- Centralized error handling
- Tested with Thunder Client, Insomnia, or `curl`

---

### 2.3 Input Validation & Error Handling

**Concepts:**
- Validation libraries: Zod (preferred), Joi, Yup
- Schema-first validation: parse, don't validate
- Distinguishing error types: validation errors, business logic errors, infrastructure errors
- Custom `AppError` class hierarchy
- Never leaking stack traces to clients in production
- Structured error responses: consistent JSON shape
- Async error propagation in Express (wrapping with `asyncHandler`)

**Industry Note:** Inconsistent error handling is one of the most common code review complaints in backend pull requests. A well-designed error system is immediately visible and respected.

**Exercises:**
1. Design an `AppError` class that carries `statusCode`, `code` (machine-readable), `message`, and `isOperational` flag.
2. Write a Zod schema for a user registration payload. Return structured validation errors that map each field to its error message.
3. Write an `asyncHandler` wrapper that catches async errors and passes them to `next()`.

---

### 2.4 Relational Databases with PostgreSQL

**Concepts:**
- Relational model: tables, rows, columns, keys, relations
- Data types: `TEXT`, `INTEGER`, `BOOLEAN`, `TIMESTAMPTZ`, `JSONB`, `UUID`
- CRUD SQL: `SELECT`, `INSERT`, `UPDATE`, `DELETE`
- Joins: `INNER`, `LEFT`, `RIGHT`, `FULL`
- Aggregations: `COUNT`, `SUM`, `AVG`, `GROUP BY`, `HAVING`
- Indexes: B-tree index, when to index, composite indexes
- Transactions: `BEGIN`, `COMMIT`, `ROLLBACK`, isolation levels
- Constraints: `NOT NULL`, `UNIQUE`, `CHECK`, `FOREIGN KEY`
- Connection pooling: why it matters, `pg-pool` configuration
- `EXPLAIN ANALYZE`: reading query plans

**Industry Note:** SQL knowledge is a career multiplier. Backend developers who can write efficient queries, design schemas, and read query plans are significantly more valuable than those who only use ORMs.

**Exercises:**
1. Design a schema for a blogging platform: users, posts, comments, tags, post_tags. Write the SQL DDL with all constraints.
2. Write a query that returns the top 10 authors by total word count of published posts. Use only SQL — no application code.
3. Add an index to a slow query. Run `EXPLAIN ANALYZE` before and after and compare the results.
4. Write a transaction that transfers "credits" between two users and rolls back if either UPDATE fails.

---

### 2.5 ORMs & Query Builders

**Concepts:**
- Prisma: schema definition, `prisma migrate`, `prisma generate`, CRUD operations
- Prisma relations: one-to-many, many-to-many, `include`, `select`
- Prisma transactions and raw SQL escape hatch
- Drizzle ORM: type-safe query builder, schema-first
- Knex.js: query builder for when you want SQL control without an ORM
- N+1 query problem and how ORMs cause it — and how to fix it

**Industry Note:** Prisma dominates modern Node.js projects. Drizzle is rapidly growing. Know how to use them effectively — but also know when to drop down to raw SQL.

**Exercises:**
1. Recreate the blogging schema in Prisma. Run migrations and seed it with sample data.
2. Write a Prisma query that retrieves all published posts with their author name and comment count — in a single database round-trip.
3. Identify and fix an N+1 query in a provided code sample.

**Mini-Project: Blog API with PostgreSQL**
- Full CRUD for users, posts, comments
- Prisma + PostgreSQL
- Zod validation on all inputs
- Pagination: cursor-based for posts list
- Soft delete for posts (set `deletedAt` rather than removing)
- Filter posts by author, tag, and status

---

### 2.6 Authentication & Authorization

**Concepts:**
- Password hashing: `bcrypt` or `argon2` — never plain text, never MD5/SHA1
- JWT: structure (header.payload.signature), signing, verifying, expiry
- Access tokens vs. refresh tokens: purpose, lifetime, storage strategy
- Cookie-based sessions vs. JWT — trade-offs
- OAuth 2.0: authorization code flow, roles, scopes
- Role-Based Access Control (RBAC): defining roles, checking permissions in middleware
- Attribute-Based Access Control (ABAC): for fine-grained authorization
- Security headers: `helmet.js` defaults explained

**Industry Note:** Auth bugs are the most consequential bugs in backend development. Understanding the WHY behind each mechanism — not just how to implement it — is what separates junior and senior developers.

**Exercises:**
1. Implement access token + refresh token rotation from scratch: issue, verify, revoke via a token blocklist in Redis.
2. Build an RBAC middleware factory: `authorize('admin', 'editor')` — it reads the role from the JWT and rejects unauthorized requests.
3. Implement Google OAuth 2.0 authorization code flow manually (no Passport.js) — exchange the code for tokens, fetch the user profile.

**Large Project: Auth Service**
- Registration with email verification (send email via Nodemailer or Resend)
- Login with access + refresh tokens
- Password reset flow (token sent via email, one-time use)
- Google OAuth login
- RBAC: `admin`, `user` roles
- Rate limiting on auth endpoints (max 5 attempts per 15 minutes)
- All endpoints tested with integration tests

---

## Phase 3 — Professional Backend Practices
### Goal: Write backend code that is maintainable, testable, observable, and deployable in real teams.

---

### 3.1 Project Architecture

**Concepts:**
- Layered architecture: Routes → Controllers → Services → Repositories → Database
- Separation of concerns: what belongs in each layer
- Dependency injection: manual DI vs. containers (tsyringe, inversify)
- Repository pattern: abstracting database access
- Domain-driven design (DDD) concepts: entities, value objects, aggregates (introduction)
- Feature-based folder structure vs. type-based
- Configuration management: `dotenv`, environment-specific configs, never commit secrets

**Industry Note:** Architecture decisions made in week one of a project determine whether it's maintainable in year three. Senior developers are hired specifically to make these decisions well.

**Exercises:**
1. Refactor a flat Express app (all code in one file) into a layered architecture. Measure the reduction in cognitive load.
2. Extract all database access from a service layer into a repository layer. Show how this makes the service testable without a real database.
3. Implement a `Config` class that reads from environment variables, validates required ones at startup, and throws descriptively if any are missing.

---

### 3.2 Testing

**Concepts:**
- Testing pyramid: unit → integration → E2E — what and how much to test at each level
- Unit testing with Vitest or Jest: pure functions, service layer with mocked dependencies
- Integration testing: testing routes against a real (test) database
- Supertest: HTTP integration testing without starting a server
- Mocking: `vi.mock`, `jest.mock`, manual mocks for external services
- Test doubles: stubs, spies, fakes — when to use each
- Database testing strategies: test database, transactions (rollback after each test), seeding
- Test coverage: what to measure, what not to obsess over
- Test-Driven Development (TDD): red → green → refactor

**Industry Note:** Untested backend code is a liability. In serious teams, PRs without tests are blocked. Start testing early — retrofitting tests onto untested code is painful.

**Exercises:**
1. Write unit tests for a `UserService.register()` method — mock the repository and email service. Cover: success, duplicate email, invalid input.
2. Write an integration test for `POST /auth/login` using Supertest. Test: valid credentials, wrong password, non-existent user, locked account.
3. Set up a test database strategy using Prisma that runs each test file in a transaction and rolls back after.

---

### 3.3 NoSQL with MongoDB

**Concepts:**
- Document model: collections, documents, BSON
- When to choose MongoDB over PostgreSQL — and when not to
- CRUD with the MongoDB Node.js driver
- Mongoose: schemas, models, virtuals, middleware (hooks)
- Schema design: embedding vs. referencing — the trade-off
- Aggregation pipeline: `$match`, `$group`, `$lookup`, `$project`, `$unwind`
- Indexes in MongoDB: single field, compound, text, TTL
- Transactions in MongoDB (replica sets)

**Exercises:**
1. Design a MongoDB schema for a social media feed. Justify the embedding vs. referencing decisions.
2. Write an aggregation pipeline that returns the top 5 most-engaged posts (likes + comments + shares) in the past 7 days.
3. Add a TTL index to a `sessions` collection so documents expire automatically after 24 hours.

---

### 3.4 Caching

**Concepts:**
- Why cache: latency reduction, database load reduction, cost savings
- Redis data structures: Strings, Hashes, Lists, Sets, Sorted Sets
- Cache patterns: Cache-Aside, Write-Through, Write-Behind, Read-Through
- Cache invalidation strategies: TTL, event-driven, cache tags
- Session storage with Redis
- Rate limiting with Redis (sliding window algorithm)
- Pub/Sub with Redis
- Cache stampede and how to prevent it (probabilistic early expiration, locks)

**Industry Note:** Redis is the most commonly used caching layer in backend systems. Knowing its data structures — not just `SET`/`GET` — opens up use cases far beyond simple caching.

**Exercises:**
1. Implement a cache-aside layer for a `GET /products/:id` endpoint. Measure response time with and without cache using `autocannon`.
2. Implement a sliding window rate limiter using Redis Sorted Sets.
3. Use Redis Pub/Sub to broadcast a message from one Node.js process and receive it in another.

**Mini-Project: Caching Layer for Blog API**
- Add Redis caching to the Blog API from Phase 2
- Cache: post list (by filter params), individual post, author profile
- Invalidate cache on write operations
- Add a cache hit/miss header to responses (`X-Cache: HIT` / `MISS`)
- Document the performance improvement

---

### 3.5 Background Jobs & Queues

**Concepts:**
- Why queues: decoupling, resilience, rate limiting, async processing
- BullMQ: jobs, queues, workers, processors
- Job lifecycle: waiting → active → completed / failed
- Retry strategies: exponential backoff, dead letter queues
- Job prioritization, delays, and repeatable (cron) jobs
- Queue monitoring with Bull Board
- When to use queues vs. cron jobs vs. event emitters

**Industry Note:** Email sending, image processing, report generation, and webhook delivery should almost always go through a queue. Blocking an HTTP response on these operations is an architectural mistake.

**Exercises:**
1. Set up BullMQ with Redis. Create a queue that sends a "welcome" email asynchronously after user registration.
2. Implement exponential backoff retry for a job that calls an unreliable external API. After 5 failures, move the job to a dead letter queue.
3. Create a repeatable job that runs every hour, generates a report, and saves it to disk.

---

### 3.6 Logging, Monitoring & Observability

**Concepts:**
- Structured logging: JSON logs, log levels, correlation IDs
- Winston or Pino (prefer Pino in production — 5–10x faster)
- Log aggregation: sending to Datadog, Grafana Loki, or AWS CloudWatch
- The three pillars of observability: logs, metrics, traces
- Metrics with Prometheus + Grafana: counters, gauges, histograms
- Distributed tracing with OpenTelemetry: traces, spans, context propagation
- Health check endpoints: `/health` and `/readiness`
- Alerting: error rate, latency (p95, p99), saturation

**Industry Note:** You cannot operate a production system you cannot observe. Observability is not optional — it is what separates hobbyist projects from production systems.

**Exercises:**
1. Replace `console.log` in an existing project with Pino. Add a correlation ID middleware that attaches a unique request ID to every log line.
2. Expose a `/metrics` endpoint in Prometheus format. Track: total requests, request duration histogram, active connections.
3. Add a `/health` endpoint that checks database connectivity and Redis connectivity — returns degraded status if either is slow.

---

## Phase 4 — Distributed Systems & Scalability
### Goal: Design and build systems that handle real production scale, failures, and complexity.

---

### 4.1 API Design at Scale

**Concepts:**
- REST best practices: versioning (`/v1/`), HATEOAS, resource naming conventions
- GraphQL: schema definition, resolvers, queries, mutations, subscriptions, DataLoader
- gRPC: Protocol Buffers, service definitions, streaming, use cases vs. REST
- API versioning strategies: URL path, header, query parameter — trade-offs
- API documentation: OpenAPI 3.0 spec, Swagger UI, automated generation
- Rate limiting: token bucket vs. leaky bucket vs. sliding window
- API gateways: Kong, AWS API Gateway — routing, auth, rate limiting, observability

**Industry Note:** GraphQL and gRPC are not replacements for REST — they solve different problems. Understanding which to reach for, and why, is a senior-level skill.

**Exercises:**
1. Document an existing REST API with OpenAPI 3.0 using `@asteasolutions/zod-to-openapi`. Serve the Swagger UI automatically.
2. Build the same endpoint in REST, GraphQL (Apollo Server), and gRPC. Benchmark and compare payload sizes and latency.
3. Implement the DataLoader pattern to solve the N+1 problem in a GraphQL resolver.

---

### 4.2 Real-Time Communication

**Concepts:**
- WebSockets: handshake, frames, connection lifecycle, heartbeat/ping-pong
- Socket.io: rooms, namespaces, acknowledgements, adapters
- Server-Sent Events (SSE): when to prefer over WebSockets
- Scaling WebSockets horizontally: the sticky session problem
- Redis adapter for Socket.io: broadcasting across multiple processes
- Long polling as a fallback

**Exercises:**
1. Build a WebSocket server that handles connection, ping/pong heartbeat, and graceful disconnection.
2. Add the Redis adapter to a Socket.io server. Run two instances of the server and verify that a message sent to one is received by clients on the other.

**Mini-Project: Real-Time Notification System**
- REST API for creating notifications
- WebSocket server delivers notifications to connected users in real-time
- If a user is offline, store notifications in the database
- On reconnect, deliver all unread notifications immediately
- Mark notifications as read via REST
- Horizontally scalable with Redis adapter

---

### 4.3 Microservices Architecture

**Concepts:**
- Monolith vs. microservices: when microservices make sense (and when they don't)
- Service decomposition: by domain, by team, by scalability requirement
- Inter-service communication: synchronous (REST, gRPC) vs. asynchronous (message broker)
- Message brokers: RabbitMQ, Apache Kafka — when to use each
- Event-driven architecture: events, publishers, subscribers, event schemas
- Saga pattern: managing distributed transactions
- Circuit breaker pattern: `opossum` library
- Service discovery and API gateway
- The fallacies of distributed computing

**Industry Note:** Most companies begin with a monolith and move toward services as they scale. Know how to work in both. Microservices solve organizational and scaling problems — they create technical complexity.

**Exercises:**
1. Implement the Circuit Breaker pattern with `opossum` around an external API call. Test it by simulating failures.
2. Publish an event to RabbitMQ from Service A and consume it in Service B. Handle failures and dead-letter routing.
3. Design (on paper) how to decompose a monolithic e-commerce app into services. Identify boundaries, shared data concerns, and communication patterns.

---

### 4.4 Message Queues & Event Streaming

**Concepts:**
- RabbitMQ: exchanges, queues, bindings, routing keys, consumers, acknowledgements
- Apache Kafka: topics, partitions, offsets, consumer groups, producers, retention
- Kafka vs. RabbitMQ: push vs. pull, ordering guarantees, replay capability
- Exactly-once vs. at-least-once vs. at-most-once delivery semantics
- Event sourcing: using events as the source of truth
- CQRS: Command Query Responsibility Segregation

**Exercises:**
1. Build a Kafka producer that publishes order events. Build two consumers: one updates inventory, one sends a confirmation email — in different consumer groups.
2. Implement at-least-once delivery with manual offset commits in Kafka. Test what happens when a consumer crashes mid-processing.

---

### 4.5 Containerization & Deployment

**Concepts:**
- Docker: images, containers, Dockerfile best practices for Node.js
- Multi-stage builds: smaller production images
- Docker Compose: local multi-service development
- Kubernetes basics: pods, deployments, services, ingress, ConfigMaps, secrets
- Horizontal Pod Autoscaler
- Health checks in Kubernetes: liveness and readiness probes
- CI/CD pipeline for Node.js: GitHub Actions → test → build image → push to registry → deploy
- Zero-downtime deployments: rolling updates, blue-green

**Industry Note:** Backend developers who can't containerize their own services create bottlenecks. Docker and basic Kubernetes knowledge is expected at mid-to-senior level.

**Exercises:**
1. Write a production-ready multi-stage Dockerfile for a Node.js app. Run the image and compare its size to a naive single-stage build.
2. Write a `docker-compose.yml` that starts your app, PostgreSQL, and Redis together with volumes and health checks.
3. Write a GitHub Actions workflow that: runs tests, builds and pushes a Docker image to GitHub Container Registry, and triggers a deployment.

---

### 4.6 Database Advanced Topics

**Concepts:**
- Database replication: primary-replica, read replicas, replication lag
- Sharding: horizontal partitioning strategies
- Connection pooling at scale: PgBouncer for PostgreSQL
- Database migrations in production: zero-downtime migration patterns
- Optimistic vs. pessimistic locking
- Full-text search: PostgreSQL `tsvector`/`tsquery` vs. Elasticsearch/Meilisearch
- Polyglot persistence: using different databases for different workloads

**Exercises:**
1. Write a zero-downtime migration that renames a column in a high-traffic table using the expand-migrate-contract pattern.
2. Implement optimistic locking using a `version` column to prevent lost updates in a concurrent update scenario.
3. Add full-text search to the Blog API using PostgreSQL's built-in capabilities. Compare query performance with and without a GIN index.

---

## Phase 5 — Security, Performance & Senior-Level Practices
### Goal: Build systems that are secure by design, performant under load, and maintainable by teams.

---

### 5.1 Security

**Concepts:**
- OWASP Top 10 for APIs (2023 edition): broken auth, excessive data exposure, mass assignment, etc.
- SQL injection: parameterized queries, ORMs as defense
- NoSQL injection in MongoDB
- XSS: output encoding, `Content-Security-Policy`
- CSRF: `SameSite` cookies, CSRF tokens
- Secrets management: never in code or `.env` committed to git — use Vault, AWS Secrets Manager
- Dependency security: `npm audit`, Snyk, Dependabot
- Security testing: `OWASP ZAP`, manual penetration testing basics
- HTTPS and TLS: certificate management, HSTS

**Industry Note:** Security is not a phase at the end of development — it's a continuous practice. One data breach ends companies and careers.

**Exercises:**
1. Audit a provided vulnerable Express app against the OWASP Top 10. Document each vulnerability and write the fix.
2. Configure `helmet.js` for a real application and explain what each header does and why it matters.
3. Set up `npm audit` and Snyk in a CI pipeline. Fail the build on high-severity vulnerabilities.

---

### 5.2 Performance Engineering

**Concepts:**
- Profiling Node.js: `--inspect`, Chrome DevTools profiler, clinic.js
- Memory leaks: identifying with heap snapshots, common causes (event listeners, closures, global caches)
- CPU profiling: finding hot paths
- Load testing: `autocannon`, k6 — designing realistic scenarios
- Connection pool sizing: the formula and why it matters
- N+1 queries at the database level: detection and fixes
- CDN for static assets and API responses
- Horizontal vs. vertical scaling decisions

**Exercises:**
1. Introduce a memory leak into a small Express app (e.g., accumulating listeners). Profile it with clinic.js Heapdump to identify the leak. Fix it.
2. Load test an API endpoint with k6. Write a test that ramps from 10 to 500 virtual users over 2 minutes. Report p95 and p99 latency.
3. Profile a slow endpoint with the Node.js inspector. Identify the hot path and optimize it.

---

### 5.3 API Documentation & Developer Experience

**Concepts:**
- OpenAPI 3.0: specification, tooling, code generation
- Generating docs automatically from Zod schemas with `zod-to-openapi`
- Changelog management: `CHANGELOG.md`, semantic versioning
- SDK generation from OpenAPI specs
- Postman collections and environments
- Webhook design: payload format, signature verification, retry behavior

**Exercises:**
1. Generate a fully documented OpenAPI spec for a CRUD API. Include examples, error responses, and authentication requirements.
2. Implement webhook signature verification using HMAC-SHA256. Build a test receiver that validates incoming webhooks.

---

### 5.4 Soft Skills & Team Practices

**Concepts:**
- Code review: what to look for, how to give and receive feedback
- Technical documentation: ADRs (Architecture Decision Records), runbooks, post-mortems
- On-call engineering: reading alerts, writing runbooks, incident response
- Estimation: breaking down tasks, communicating uncertainty
- Technical debt: identifying, quantifying, prioritizing
- Mentoring junior developers

**Exercises:**
1. Write an ADR for a technology choice you've made in one of your projects (e.g., "Why we chose PostgreSQL over MongoDB").
2. Write a post-mortem for a bug you introduced (real or simulated) — include timeline, root cause, impact, and prevention measures.

---

## Large Capstone Project: Production-Grade SaaS Backend

### Project: Multi-Tenant Task Management API

This project consolidates everything across all five phases.

**Domain:**
A task management system where organizations have workspaces, users have roles, and tasks move through a workflow.

**Requirements:**

**Core Features:**
- Multi-tenancy: organizations with isolated data
- User auth: registration, email verification, login, refresh tokens, password reset, Google OAuth
- RBAC: `owner`, `admin`, `member`, `viewer` roles per organization
- Projects, tasks, subtasks, comments, file attachments
- Task assignment, due dates, priority, labels, status workflow
- Real-time updates via WebSockets (task status changes, new comments)
- Notifications: in-app + email via queue

**Advanced Features:**
- Full-text search on tasks and comments
- Activity log / audit trail for all mutations
- Background jobs: email delivery, file processing, digest emails
- Rate limiting per organization and per user
- Webhook delivery with retry and signature verification
- API versioning (`/v1/`)
- OpenAPI documentation auto-generated

**Technical Requirements:**
- TypeScript throughout
- Node.js + Fastify (or Express)
- PostgreSQL with Prisma
- Redis for caching, rate limiting, sessions, queues (BullMQ)
- Socket.io with Redis adapter (horizontally scalable)
- Containerized with Docker Compose (app + postgres + redis)
- GitHub Actions CI: lint + test + build + push image
- 80%+ test coverage on service layer
- Structured logging with Pino + correlation IDs
- Health check and metrics endpoints

**Deliverables:**
- Public GitHub repository with a production-quality README
- Full OpenAPI documentation served via Swagger UI
- Postman collection for all endpoints
- Architecture decision records for at least 3 key choices
- Load test results with k6

---

## Supplementary Skills (Integrate Throughout)

| Skill | When to Learn | Tools |
|---|---|---|
| Bash scripting | Phase 1 | Bash, zsh |
| SQL advanced | Phase 2–3 | PostgreSQL |
| Linux fundamentals | Phase 2 | Ubuntu, SSH |
| Networking basics | Phase 3 | TCP/IP, DNS, TLS |
| Cloud basics | Phase 4 | AWS or GCP free tier |
| Infrastructure as Code | Phase 4 | Terraform basics |
| API security | Phase 5 | OWASP, Burp Suite |

---

## Resource Index

### Node.js & JavaScript
- [Node.js official docs](https://nodejs.org/en/docs/) — always the primary reference
- *Node.js Design Patterns* by Mario Casciaro & Luciano Mammino — the essential Node.js book
- [javascript.info](https://javascript.info) — best free JS resource
- [Node.js Best Practices](https://github.com/goldbergyoni/nodebestpractices) — GitHub repo, continuously updated

### TypeScript
- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
- [Total TypeScript](https://www.totaltypescript.com) — free workshops by Matt Pocock

### Databases
- *Learning SQL* by Alan Beaulieu
- [Use The Index, Luke](https://use-the-index-luke.com) — SQL indexing explained
- [Prisma docs](https://www.prisma.io/docs)

### System Design
- *Designing Data-Intensive Applications* by Martin Kleppmann — the most important backend book
- [System Design Primer](https://github.com/donnemartin/system-design-primer) — free GitHub resource
- [ByteByteGo Newsletter](https://blog.bytebytego.com)

### Security
- [OWASP API Security Top 10](https://owasp.org/www-project-api-security/)
- [PortSwigger Web Security Academy](https://portswigger.net/web-security) — free, hands-on

### Performance & Observability
- [clinic.js](https://clinicjs.org) — Node.js performance profiling
- [OpenTelemetry for Node.js](https://opentelemetry.io/docs/instrumentation/js/)
- [k6 docs](https://k6.io/docs/)

---

## Progress Checkpoints

### After Phase 1
- [ ] Can explain the event loop and why blocking it is catastrophic
- [ ] Comfortable with `async`/`await`, Promises, and async error handling
- [ ] Can use Node's `stream`, `crypto`, `fs`, and `events` modules fluently
- [ ] Built the File Processing CLI

### After Phase 2
- [ ] Can design and build a REST API with proper HTTP semantics from scratch
- [ ] Comfortable with PostgreSQL schema design, indexes, and transactions
- [ ] Can implement auth (JWT, refresh tokens, OAuth) without a library doing it for them
- [ ] Built and tested the Auth Service

### After Phase 3
- [ ] Can architect a layered, testable codebase and explain why each layer exists
- [ ] Writes integration tests as a default, not an afterthought
- [ ] Understands Redis well enough to use it for caching, queues, and rate limiting
- [ ] Has observable applications: structured logs, metrics, health checks

### After Phase 4
- [ ] Can decompose a system into services and reason about the trade-offs
- [ ] Understands Kafka vs. RabbitMQ and can pick the right tool
- [ ] Can containerize and deploy a multi-service application
- [ ] Has designed a system with real-time capabilities that scales horizontally

### After Phase 5
- [ ] Can audit an application for OWASP vulnerabilities and fix them
- [ ] Can profile and fix a memory leak or CPU bottleneck
- [ ] Has shipped a capstone project to production and written documentation for it
- [ ] Can write an ADR and a post-mortem

---

*Built for developers who want to work in the industry, not just pass interviews. Focus on shipping real things.*