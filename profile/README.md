# Agent Runtime Control Protocol

ARCP is a transport-agnostic wire protocol for **running agents** — authenticating sessions, scheduling durable jobs, streaming results, keeping humans in the loop, and auditing every state transition.

<p align="center">
  <img src="https://img.shields.io/badge/spec-1.0-blue" alt="Spec version" />
  <img src="https://img.shields.io/badge/license-Apache--2.0-green" alt="License" />
  <img src="https://img.shields.io/badge/SDKs-11-blue" alt="Reference SDKs" />
</p>

## What's in the box

- **Authenticated sessions** with capability negotiation, durable reconnect, and credential rotation.
- **Durable jobs** that heartbeat, checkpoint, and resume across transport drops.
- **Typed streams** — text, binary, events, logs, metrics, and reasoning — sharing one backpressure contract.
- **Cooperative cancel + interrupt**, distinct from termination, so humans can guide work mid-flight.
- **Lease-scoped permissions** that are time-boxed, revocable, and explicit at every trust boundary.
- **First-class human-in-the-loop** primitives: typed input prompts, choice pickers, default-on-expiry.
- **Addressable artifacts** for results, shared memory, and large or binary payloads.
- **Read-only observer subscriptions** for dashboards, audit, and replay — built in, not bolted on.
- **Multi-agent delegation and handoff** that preserves `trace_id` and inherits scoped permissions.
- **Canonical error taxonomy** and reserved metric names, so dashboards and alerts port across runtimes.

## Reference SDKs

Eleven first-party SDKs track the same spec version. Pick the one closest to your stack.

| Language   | Repo                                                                              | Package                                                |
| ---------- | --------------------------------------------------------------------------------- | ------------------------------------------------------ |
| TypeScript | [`typescript-sdk`](https://github.com/agentruntimecontrolprotocol/typescript-sdk) | `arcp` (npm)                                           |
| Python     | [`python-sdk`](https://github.com/agentruntimecontrolprotocol/python-sdk)         | `arcp` (PyPI)                                          |
| Go         | [`go-sdk`](https://github.com/agentruntimecontrolprotocol/go-sdk)                 | `github.com/agentruntimecontrolprotocol/go-sdk`        |
| Rust       | [`rust-sdk`](https://github.com/agentruntimecontrolprotocol/rust-sdk)             | `arcp` (crates.io)                                     |
| Java       | [`java-sdk`](https://github.com/agentruntimecontrolprotocol/java-sdk)             | `dev.fizzpop:arcp` (Maven)                             |
| Kotlin     | [`kotlin-sdk`](https://github.com/agentruntimecontrolprotocol/kotlin-sdk)         | `dev.arcp:lib` (Maven)                                 |
| Swift      | [`swift-sdk`](https://github.com/agentruntimecontrolprotocol/swift-sdk)           | `ARCP` (SwiftPM)                                       |
| Ruby       | [`ruby-sdk`](https://github.com/agentruntimecontrolprotocol/ruby-sdk)             | `arcp` (RubyGems)                                      |
| PHP        | [`php-sdk`](https://github.com/agentruntimecontrolprotocol/php-sdk)               | `arcp/arcp` (Packagist)                                |
| C#         | [`csharp-sdk`](https://github.com/agentruntimecontrolprotocol/csharp-sdk)         | `ARCP` (NuGet)                                         |
| F#         | [`fsharp-sdk`](https://github.com/agentruntimecontrolprotocol/fsharp-sdk)         | `ARCP.FSharp` (NuGet)                                  |

Each SDK ships runnable examples; the canonical wire format and lifecycle live in [`.github/README.md`](https://github.com/agentruntimecontrolprotocol/.github/blob/main/README.md).

## Where to start

- Building against the protocol? Read [the protocol README](https://github.com/agentruntimecontrolprotocol/.github/blob/main/README.md) and pick an SDK above.
- Curious about the wire shape? The envelope, message types, and session lifecycle are documented end-to-end with examples.
- Want to contribute? Spec changes go through RFCs in this org; SDK changes go through each SDK repo.

## License

Specification text under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/); reference implementations under [Apache-2.0](https://www.apache.org/licenses/LICENSE-2.0).
