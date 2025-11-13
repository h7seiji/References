# System Design Playbook

## 0–2 min — Frame & align

Say: “I’ll clarify scope and success metrics, then propose a high-level design, data model & APIs, scaling, consistency, and failure modes.”

- Scope: core features, out-of-scope (nice-to-haves).
- SLOs: p99 latency targets, availability, data freshness.
- Scale assumptions: DAU, QPS, data sizes, growth.

## 2–5 min — Back-of-the-envelope sizing

Quick numbers keep you grounded:

- Reads/QPS: DAU × actions/user ÷ secondsActive
- Writes/day: e.g., uploads/likes/comments.
- Storage/day: events/day × bytes/event (+30% overhead).
- Bandwidth: RPS × payload (ingress/egress).
- Connection count: for realtime (WebSockets) ≈ concurrent users.

Say: the assumptions out loud; adjust if interviewer pushes back.

## 5–10 min — High-level architecture (whiteboard)

Boxes & arrows (keep it legible):

- Edge: CDN, WAF, API GW/LB, AuthN/AuthZ, rate limiting.
- Services: Upload, Feed, User/Social Graph, Notifications, Media Processing, Search.
- Async: Queue/Stream (Kafka/Kinesis), workers, schedulers.
- Data: Object Store (photos) + CDN; SQL (accounts/billing), NoSQL (feeds/likes), Graph DB (follows); Cache (Redis); Search (Elastic/Opensearch).
- Observability: logs/metrics/traces; feature flags; config.

### Anchor phrases

“Binary blobs in object storage; metadata in DBs suited to access patterns.”
“Write path async where possible; read path fast and cache-friendly.”

## 10–15 min — Data model & APIs (show you can ship)

Entities (example): User, Photo, Follow, Like, Comment, FeedItem.

- SQL (normalized where it matters): users(id, handle, …), sessions, billing.
- NoSQL (wide tables by access paths): feed_by_user(user_id, ts DESC → photo_id, author_id), likes_by_photo(photo_id, ts DESC → user_id).
- Graph: follows(src_user, dst_user, ts).

### API sketch (idempotent where needed)

- POST /photos (idempotency-key) → returns photo_id, URLs.
- GET /feed?cursor=... (keyset pagination).
- POST /likes (idempotent on {user_id, photo_id}).
- POST /follows, DELETE /follows/{id}.
- GET /users/{id}; GET /photos/{id}.

## 15–22 min — Scaling & trade-offs (show judgment)

### Caching strategy

- Hot reads in Redis: feed pages, user profiles, like counts (with TTL + versioned keys).
- Stampede control: single-flight locks or background refresh.

### Feed computation

- Start fan-out on read (simple). Evolve to hybrid: precompute for normal users via stream consumers; keep celebs as pull-on-read.
- Ordering: write time; tie-breaker by photo_id; keyset pagination.

### Sharding

- By user_id (hash) for per-user data (feeds, profiles).
- By photo_id (hash) for photo-centric writes (likes/comments).
- Directory/lookup service to allow live rebalancing.

### Consistency

- User actions (likes/comments): eventual consistency is fine; expose “optimistic UI,” reconcile on server confirmation.
- Money/security-critical: strong consistency (SQL, transactions).
- Cross-DC: async replication; accept read-after-write lag or route sticky reads.

### Protocols

- Client→edge: HTTP/2 (multiplexing), HTTP/3 if available.
- Realtime user notifications: WebSockets/SSE.
- Service→service: gRPC (unary + streaming) with deadlines & retries.

## 22–27 min — Reliability & ops (the “grown-up” stuff)

### Resilience

- Timeouts, retries with jittered exponential backoff.
- Idempotency keys on POSTs (uploads, likes).
- Circuit breakers + bulkheads (shed load gracefully).
- DLQs for poisoned messages; replayability from the stream.

### Observability

- RED/USE metrics; traces with OpenTelemetry; structured logs w/ correlation IDs.
- SLOs: e.g., p99 feed ≤ 500ms, upload ≤ 2s, availability 99.9%.
- Canary + auto-rollbacks; feature flags for risky paths (e.g., fanout).

### Security

- OAuth2/OIDC; scoped tokens; service mTLS; least privilege IAM.
- Input validation; rate limits per IP/user/app; abuse detection (like floods, follow spam).

## 27–30 min — Evolution plan & trade-off recap

- Phase 1 (MVP): fan-out on read, single region, read replicas, Redis cache, S3+CDN, basic analytics.
- Phase 2: streams + consumers (precompute feeds), multi-region read, warm caches, background media pipelines.
- Phase 3: multi-region active/active, partitioned trending, tiered storage, cost optimizations.

Close with crisp trade-offs you made (e.g., eventual consistency on likes to hit latency SLO; hybrid storage to match access patterns; hybrid feed to manage celebrity fanout).

## Cheat sheets you can glance at

### Keyset vs offset pagination

- Offset: simple, slow at high offsets, unstable.
- Keyset: fast, stable; needs sortable unique key (ts, id).

### Cache write policies

- Write-through: strong-ish, slower writes.
- Write-around: fast writes, possibly stale reads.
- Write-back: fastest writes, risk on crash; use only with durable queues.

### Sharding quick picks

- Hash: uniform load; bad for ranges.
- Range: great for scans; hotspot risk; add time-bucketed ranges to distribute hot keys.
- Directory: flexible rebalancing; extra hop.

### Rate limiting

- Token bucket at edge per user/app/IP; separate “hot endpoints” (likes).
- Return 429 with Retry-After; degrade to cached or partial results.
- Back-of-envelope latency budget (feed read p99 500ms)
- Edge/CDN/auth: 50–80ms
- Service + cache hit: 50–100ms
- DB/NoSQL read(s): 100–200ms (aim for cache hit >90%)
- Network wiggle room: 50–100ms → If cache miss paths exceed budget, precompute or add read-through cache.

### Failure drills

- Primary DB down → read-only mode + banner; queue writes for later.
- Cache cluster fail → elevated DB load; enable adaptive TTLs & request coalescing.
- Stream consumer lag → pause non-critical fanouts; prioritize “new post” over “like count.”
