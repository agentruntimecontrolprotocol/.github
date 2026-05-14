# ARCP — Agent Runtime Control Protocol

A transport-agnostic wire protocol for submitting, observing, and controlling long-running AI agent jobs.

**Current draft:** v1 — Standards Track — expires November 13, 2026

## What it is

ARCP defines the durable execution envelope around AI agent work: sessions, jobs, resumable event streams, capability-bounded leases, and delegation. It stays agnostic about agent implementation and tool transport — MCP exposes tools, OpenTelemetry handles telemetry export, and ARCP composes with both.

Four concerns, scoped tightly:

- **Identity** — who is talking, what session, what trace
- **Durability** — resumable streams, gap-free sequencing, idempotent submission
- **Authority** — leases over filesystem, network, tools, sub-agents, and cost
- **Observability** — structured events, progress, metrics, streamed results

## Features

- **Sessions** — authenticated, resumable, with capability negotiation in `session.hello` / `session.welcome`
- **Liveness** — explicit `session.ping` / `session.pong` heartbeats (§6.4)
- **Flow control** — `session.ack` for window-based event acknowledgement (§6.5)
- **Introspection** — `session.list_jobs` for read-only job inventory (§6.6)
- **Idempotent submission** — `idempotency_key` on `job.submit` for safe retries
- **Subscription** — `job.subscribe` to attach to a running job from a different session, without inheriting cancel authority (§7.6)
- **Agent versioning** — `name@version` identifiers with inventory advertised in `session.welcome` (§7.5)
- **Leases** — capability-bounded authority over `fs.*`, `net.fetch`, `tool.call`, `agent.delegate`
- **Time-bounded authority** — `lease_constraints.expires_at` (§9.5)
- **Budget enforcement** — `cost.budget` capability with runtime-maintained counters and per-currency tracking (§9.6)
- **Delegation** — sub-agent jobs with strict lease subsetting (§10)
- **Progress reporting** — structured `progress` events (§8.2)
- **Result streaming** — `result_chunk` events for large outputs (§8.4)
- **Trace propagation** — W3C Trace Context across sessions, jobs, and delegations (§11)
- **Fifteen-code error taxonomy** — including `BUDGET_EXHAUSTED`, `LEASE_EXPIRED`, `AGENT_VERSION_NOT_AVAILABLE` (§12)

## Non-goals

Out of scope, deliberately:

- Agent implementation
- Tool exposure (use MCP)
- HITL UX
- Agent state persistence across process restarts
- Telemetry export (use OpenTelemetry)
- Auth mechanisms beyond bearer tokens
- Scheduling, priority, federation, pause/resume, LLM token streaming — deferred

## Reference SDKs

Eleven first-party SDKs track the same spec version. Pick the one closest to your stack.

| Language    | Repo                                                                              |
| ----------- | --------------------------------------------------------------------------------- |
| TypeScript  | [`typescript-sdk`](https://github.com/agentruntimecontrolprotocol/typescript-sdk) |
| Python      | [`python-sdk`](https://github.com/agentruntimecontrolprotocol/python-sdk)         |
| Go          | [`go-sdk`](https://github.com/agentruntimecontrolprotocol/go-sdk)                 |
| Rust        | [`rust-sdk`](https://github.com/agentruntimecontrolprotocol/rust-sdk)             |
| Java        | [`java-sdk`](https://github.com/agentruntimecontrolprotocol/java-sdk)             |
| Kotlin      | [`kotlin-sdk`](https://github.com/agentruntimecontrolprotocol/kotlin-sdk)         |
| Swift       | [`swift-sdk`](https://github.com/agentruntimecontrolprotocol/swift-sdk)           |
| Ruby        | [`ruby-sdk`](https://github.com/agentruntimecontrolprotocol/ruby-sdk)             |
| PHP         | [`php-sdk`](https://github.com/agentruntimecontrolprotocol/php-sdk)               |
| C#          | [`csharp-sdk`](https://github.com/agentruntimecontrolprotocol/csharp-sdk)         |
| F#          | [`fsharp-sdk`](https://github.com/agentruntimecontrolprotocol/fsharp-sdk)         |

## Spec

The full draft lives in [`SPEC.md`](https://github.com/agentruntimecontrolprotocol/.github/blob/main/SPEC.md).

| Section | Contents                                                                          |
| ------- | --------------------------------------------------------------------------------- |
| §1–2    | Introduction, conventions, terminology                                            |
| §3–5    | Protocol overview, transport, wire format                                         |
| §6      | Sessions: hello/welcome, resume, heartbeats, ack, listing                         |
| §7      | Jobs: lifecycle, cancellation, versioning, subscription                           |
| §8      | Events: kinds, ordering, result streaming                                         |
| §9      | Leases: grammar, enforcement, subsetting, expiration, budget                      |
| §10–11  | Delegation, trace propagation                                                     |
| §12     | Error taxonomy                                                                    |
| §13     | Worked examples (heartbeat, ack/back-pressure, subscribe, expiration, budget, chunked result, versioning) |
| §14     | Security considerations                                                           |

## Status

Draft specification distributed for review. Implementations are encouraged but should expect breaking changes before v1 is finalized. The wire format is the contract — anything not specified here is implementation-defined.

Capability negotiation is the forward-compatibility story: both peers advertise a `features` list in `session.hello` / `session.welcome`, and the effective feature set is their intersection. New features land behind new flags so older clients keep working.

## Contributing

Issues and pull requests welcome. For protocol-level changes, open an issue first to discuss intent before sending a PR — once a feature flag ships in a registered implementation it is effectively frozen.

When proposing changes, please indicate:

1. Which section(s) are affected
2. Whether the change is backward-compatible with the feature-negotiation rules in §6.2
3. Whether it introduces a new feature flag, error code, event kind, or capability namespace (these require IANA-registry coordination per §15)

## License

[TBD]
