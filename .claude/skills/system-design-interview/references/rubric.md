# System Design Interview Rubric

Internal reference for the agent. Not shown to the candidate during the session.

---

## Basic Design Completeness Checklist (Phase 3 Gate)

The agent considers the basic design sufficient when the candidate has addressed **all** of the following. Each item must be addressed — not just mentioned in passing.

| # | Item | What counts as addressed |
|---|------|--------------------------|
| 1 | Functional scope | Candidate stated what the system does and explicitly scoped what it does NOT do |
| 2 | Scale target | Concrete numbers: DAU, QPS, or data volume — not just "large scale" |
| 3 | Non-functional priority | At least one explicit priority with a stated reason (e.g., "we prefer availability over consistency because reads can tolerate staleness") |
| 4 | End-to-end happy path | Candidate walked through a complete request flow from client to storage and back |
| 5 | Storage layer choice with rationale | Named a specific storage type (SQL, NoSQL, blob, time-series, etc.) and gave a reason |
| 6 | At least one failure mode | Identified what breaks and what the system does about it (retry, failover, degraded mode, etc.) |

If any item is unaddressed when the candidate signals completion, the agent probes specifically for that item — not generically.

---

## Deep Dive Sub-Domain Selection Guide (Phase 4)

Pick 2–3 sub-domains based on the problem type. Prioritize the ones where a shallow answer is a deal breaker.

| Problem Type | Priority Sub-Domains |
|---|---|
| Search / Autocomplete | Index structure (trie or inverted index), storage and serialization of index, query ranking, incremental update strategy |
| Rate Limiter | Algorithm choice (token bucket vs. sliding window log vs. sliding window counter), distributed counter synchronization, edge cases at boundary |
| Newsfeed / Timeline | Fan-out strategy (push vs. pull vs. hybrid), feed storage and pagination, cache invalidation on follow/unfollow |
| URL Shortener | Hash collision handling, redirect mechanism (301 vs. 302), analytics without blocking the hot path, storage estimation |
| Key-Value Store | Consistency model (strong vs. eventual), replication strategy, conflict resolution, compaction |
| Notification System | Delivery guarantees (at-least-once vs. exactly-once), fan-out at scale, retry and dead-letter handling, multi-channel routing |
| Distributed Crawler | Politeness constraints (robots.txt, rate limiting per domain), URL deduplication at scale, frontier prioritization, distributed coordination |
| Distributed Cache | Eviction policy (LRU, LFU, TTL), cache stampede mitigation, consistency modes (write-through, write-behind, cache-aside) |
| Payment / Transaction System | Idempotency keys, two-phase commit vs. saga pattern, reconciliation, audit logging |
| Chat / Messaging | Message ordering guarantees, delivery receipts, presence system, storage vs. ephemeral trade-off |

For problems not listed: prioritize the sub-domains where the core intellectual challenge lives — usually the part that seems simple but breaks at scale.

---

## Deal Breaker Identification Guide (Phase 5 Summary)

A deal breaker is a design decision where:
1. It is the core intellectual challenge of the problem
2. A surface-level or textbook answer (correct but naive) would indicate the candidate hasn't thought about scale or real-world constraints
3. A No Hire is justified even if the rest of the design is strong

**Test:** *"If the candidate answered everything else brilliantly but gave a shallow answer here, would a panel still reject them?"* If yes, it's a deal breaker.

### Examples by problem type

| Problem | Deal Breaker |
|---|---|
| Autocomplete | How the trie is stored on disk and served at scale — in-memory per node is a non-starter; must address serialization, sharding, or prefix-to-shard mapping |
| Rate Limiter | How the distributed counter stays consistent across nodes without a central bottleneck — a Redis-based answer must address failure and clock skew |
| Newsfeed | Fan-out strategy at celebrity-follower scale — naive push-to-all fails; candidate must address hybrid fan-out or pull-on-read for high-fan-out accounts |
| URL Shortener | Collision handling at billions of URLs — must address probability, retry strategy, and whether the hash space is sufficient |
| Chat | Message ordering in a distributed system — per-sender sequence numbers vs. global ordering; tradeoffs of each |
| Distributed Cache | Cache stampede (thundering herd) on popular key expiry — must address probabilistic early expiry, mutex locks, or background refresh |

**Generic statements that are NOT deal breakers:**
- "Consider scalability" (too vague)
- "Handle failures gracefully" (not specific)
- "Use caching to reduce load" (a general principle, not the core challenge)

Deal breakers in the summary must be specific enough that the candidate knows exactly what they need to study.
