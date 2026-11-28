# PRAXO-CORE for Java

PRAXO-CORE (also written praxocore) is an embeddable, MIT-licensed agent framework. Java implementation of the PRAXO-CORE contract. The normative contract is [`spec/`](https://github.com/axisvela/praxo-core/blob/main/spec/README.md); Go remains the reference implementation.

## At a glance

| Field | Value |
| --- | --- |
| Package | `com.axisvela:praxo-core` |
| Registry | [Maven Central](https://repo1.maven.org/maven2/com/axisvela/praxo-core/0.12.3/) |
| Install | `Maven: com.axisvela:praxo-core:0.12.3` |
| Source version | `0.12.3` |
| Published version | `0.12.3` |
| Publication status | published |
| Canonical source tag | [`java/v0.12.3`](https://github.com/axisvela/praxo-core/tree/java/v0.12.3) |
| Tier | Core |
| Contract | `SPEC_VERSION` `0.2.0` |
| Documentation | https://axisvela.github.io/praxo-core/languages/java/ |
| License | MIT |

## Highlights

- OpenAI-compatible model: native
- Anthropic model: native
- Gemini model: native
- MCP client: native
- Harmovela sink: native
- OpenTelemetry sink: native (transport seam)
- Subagent delegation: native
- Retriever: native

## Quick start

Install the published package:

```text
Maven: com.axisvela:praxo-core:0.12.3
```

```java
import com.axisvela.praxo.agent.Agent;
import com.axisvela.praxo.agent.AgentOptions;
import com.axisvela.praxo.agent.Session;
import com.axisvela.praxo.model.Message;
import com.axisvela.praxo.model.Request;
import com.axisvela.praxo.model.Response;
import com.axisvela.praxo.tool.FuncTool;
import com.axisvela.praxo.tool.Registry;

var tools = new Registry();
tools.register(new FuncTool("echo", "Echo", args -> args));

var agent = new Agent(new AgentOptions(request -> Response.of(
        Message.assistant("hello", java.util.List.of()))));
var result = agent.run(new Session("session-1"), "hi");
System.out.println(result.output + " " + result.steps);
```

See the [full Java README](language/java/README.md) for complete installation, build, and verification commands.

## What's included

| Capability | Status | Detail |
| --- | --- | --- |
| OpenAI-compatible model | native | `adapters.OpenAICompatibleModel` |
| Anthropic model | native | `adapters.AnthropicModel`; SSE streaming reassembly |
| Gemini model | native | `adapters.GeminiModel`; SSE streaming |
| MCP client | native | `adapters.McpClient`; stdio, plus `McpStreamableHttpTransport` for Streamable HTTP 2025-03-26 (local runtime verification pending) |
| Harmovela sink | native | `adapters.HarmovelaSink` |
| OpenTelemetry sink | native (transport seam) | `adapters.OtelSink`; caller supplies OTLP/HTTP transport |
| Subagent delegation | native | `agent.delegation.SubagentManager` |
| Retriever | native | `retriever.Document` and `Retriever` |

## Examples

Runnable examples live under [`language/java/examples`](language/java/examples).

| Example | What it shows |
| --- | --- |
| [advanced-delegation](language/java/examples/advanced-delegation) | This example shows an application-level parent/child agent pattern. The parent agent may call a `delegate` tool but not the child's `record` tool. The delegate tool runs a child agent with its own tool scope, policy, and fixture model. |
| [checkpoint](language/java/examples/checkpoint) | This example uses published Maven `com.axisvela:praxo-core:0.7.0` to keep checkpoint storage application-owned while using the SDK allowlist for payload encoding. |
| [consumer](language/java/examples/consumer) | This starter installs the published `com.axisvela:praxo-core:0.12.3` artifact from Maven Central in a separate application. It does not compile or import the repository's Java source. Java 21 or newer and Maven 3.9 or newer are required. PRAXO-CORE has no runtime dependencies. |
| [event-sink](language/java/examples/event-sink) | This example uses published Maven `com.axisvela:praxo-core:0.7.0` to observe agent lifecycle and tool events without coupling the agent to a logging or telemetry backend. |
| [hitl](language/java/examples/hitl) | This example uses published Maven Central `com.axisvela:praxo-core:0.9.0` to approve one write, then edit it to a target that the policy rejects. |
| [identity-policy](language/java/examples/identity-policy) | This example uses published Maven `com.axisvela:praxo-core:0.7.0` to bind a trusted principal to Core policy authorization. The application owns authentication and principal storage; Core only calls the policy hook. |
| [live-model](language/java/examples/live-model) | This example uses published Maven Central `com.axisvela:praxo-core:0.9.0` to connect the Java Core to an OpenAI-compatible endpoint and registers one low-risk `get_time` tool. |
| [mcp](language/java/examples/mcp) | This example uses published Maven `com.axisvela:praxo-core:0.7.0` with an in-process `McpTransport`. It needs no server process and no network endpoint. |
| [provider-fallback](language/java/examples/provider-fallback) | This example uses published Maven `com.axisvela:praxo-core:0.7.0` to fall back to a second model when the primary model call fails. |
| [representative-chain](language/java/examples/representative-chain) |  |
| [retry](language/java/examples/retry) | This example uses published Maven `com.axisvela:praxo-core:0.7.0` to retry transient model failures without changing the agent loop. |
| [service](language/java/examples/service) | This example embeds published Maven `com.axisvela:praxo-core:0.7.0` in a standard-library JDK HTTP service. The application supplies a principal and tenant, restricts tools, and returns JSON. |
| [session-checkpoint](language/java/examples/session-checkpoint) | This example uses published Maven Central `com.axisvela:praxo-core:0.9.0` and the checkpoint allowlist to save, restore, and continue a multi-turn session. |
| [streaming](language/java/examples/streaming) | This example uses published Maven `com.axisvela:praxo-core:0.7.0` to consume deltas while the agent loop keeps running normally. |
| [structured-output](language/java/examples/structured-output) | This example uses published Maven Central `com.axisvela:praxo-core:0.9.0` to turn free text into validated JSON with `StructuredOutput`. |

## Scenario Tutorials

Scenario-oriented tutorials live under `language/java/Tutorial`. Planning context: [Tutorial Plan](https://axisvela.github.io/praxo-core/getting-started/tutorial-plan/), [100 candidate agent scenarios](https://axisvela.github.io/praxo-core/getting-started/agent-scenarios/), and [Tutorial Catalog](https://axisvela.github.io/praxo-core/getting-started/tutorial-catalog/).

| Path | What it shows |
| --- | --- |
| [Tutorial](language/java/Tutorial) | Application tutorials live in `Tutorial/`, alongside focused `language/go/examples/`. |
| [airport-recovery](language/java/Tutorial/airport-recovery) | A bounded tutorial slice over the native Java Core. It reads one fixed fixture, enforces scope and drafts a review-only result. No production write or external system access. |
| [api-orchestration](language/java/Tutorial/api-orchestration) | A bounded tutorial slice over the native Java Core. It reads one fixed fixture, enforces scope and drafts a review-only result. No production write or external system access. |
| [architecture-graph](language/java/Tutorial/architecture-graph) | A bounded tutorial slice over the native Java Core. It reads one fixed fixture, enforces scope and drafts a review-only result. No production write or external system access. |
| [budget-review](language/java/Tutorial/budget-review) | A bounded tutorial slice over the native Java Core. It reads one fixed fixture, enforces scope and drafts a review-only result. No production write or external system access. |
| [clinical-guidelines](language/java/Tutorial/clinical-guidelines) | A bounded tutorial slice over the native Java Core. It reads one fixed fixture, enforces scope and drafts a review-only result. No production write or external system access. |
| [container-yard](language/java/Tutorial/container-yard) | A bounded tutorial slice over the native Java Core. It reads one fixed fixture, enforces scope and drafts a review-only result. No production write or external system access. |
| [credit-diligence](language/java/Tutorial/credit-diligence) | A bounded tutorial slice over the native Java Core. It reads one fixed fixture, enforces scope and drafts a review-only result. No production write or external system access. |
| [customs-reroute](language/java/Tutorial/customs-reroute) | A bounded tutorial slice over the native Java Core. It reads one fixed fixture, enforces scope and drafts a review-only result. No production write or external system access. |
| [due-diligence](language/java/Tutorial/due-diligence) | A bounded tutorial slice over the native Java Core. It reads one fixed fixture, enforces scope and drafts a review-only result. No production write or external system access. |
| [legacy-migration](language/java/Tutorial/legacy-migration) | A bounded tutorial slice over the native Java Core. It reads one fixed fixture, enforces scope and drafts a review-only result. No production write or external system access. |
| [medical-coding](language/java/Tutorial/medical-coding) | A bounded tutorial slice over the native Java Core. It reads one fixed fixture, enforces scope and drafts a review-only result. No production write or external system access. |
| [order-review](language/java/Tutorial/order-review) | This tutorial embeds the native Java Core in a loopback HTTP application. It uses the same synthetic business service as Python and TypeScript, not a shared remote Agent. The initial model is deterministic: it requests `review_order`, then returns the tool result. The application computes the recommendation from order status. It does not use an LLM to decide a refund or perform business writes. |
| [patent-fto](language/java/Tutorial/patent-fto) | A bounded tutorial slice over the native Java Core. It reads one fixed fixture, enforces scope and drafts a review-only result. No production write or external system access. |
| [precedent-outline](language/java/Tutorial/precedent-outline) | A bounded tutorial slice over the native Java Core. It reads one fixed fixture, enforces scope and drafts a review-only result. No production write or external system access. |
| [public-approval](language/java/Tutorial/public-approval) | A bounded tutorial slice over the native Java Core. It reads one fixed fixture, enforces scope and drafts a review-only result. No production write or external system access. |
| [rpa-reconciliation](language/java/Tutorial/rpa-reconciliation) | A bounded tutorial slice over the native Java Core. It reads one fixed fixture, enforces scope and drafts a review-only result. No production write or external system access. |
| [supply-disruption](language/java/Tutorial/supply-disruption) | A bounded tutorial slice over the native Java Core. It reads one fixed fixture, enforces scope and drafts a review-only result. No production write or external system access. |
| [tax-review](language/java/Tutorial/tax-review) | A bounded tutorial slice over the native Java Core. It reads one fixed fixture, enforces scope and drafts a review-only result. No production write or external system access. |
| [tender-review](language/java/Tutorial/tender-review) | A bounded tutorial slice over the native Java Core. It reads one fixed fixture, enforces scope and drafts a review-only result. No production write or external system access. |
| [test-generation](language/java/Tutorial/test-generation) | A bounded tutorial slice over the native Java Core. It reads one fixed fixture, enforces scope and drafts a review-only result. No production write or external system access. |
| [trial-screening](language/java/Tutorial/trial-screening) | A bounded tutorial slice over the native Java Core. It reads one fixed fixture, enforces scope and drafts a review-only result. No production write or external system access. |
| [wealth-service](language/java/Tutorial/wealth-service) | A native Java Core tutorial for a review-only wealth workflow. The Agent has two fixed tools: `read_portfolio` reads synthetic account `acct-100`, and `draft_rebalance` produces a `draft_only` allocation proposal for human review. It never places a trade, transfers cash or changes a portfolio. |
| [zero-trust-review](language/java/Tutorial/zero-trust-review) | A bounded tutorial slice over the native Java Core. It reads one fixed fixture, enforces scope and drafts a review-only result. No production write or external system access. |

## Reference Applications

Reference application sources live under `language/java/application`. See each README for implementation scope and validation status.

| Path | What it shows |
| --- | --- |
| [application](language/java/application) | A Spring Boot commerce application where the agent drives the primary shopping workflow: a customer states an intent, the agent searches the application-owned catalog, checks inventory, drafts a cart, and creates a review-only checkout request. The agent never charges, places an order, or ships. |

## Verify

Run the checks from `language/java`:

```bash
cd language/java
mvn -q -DskipTests test-compile
mvn -q -DskipTests package
java -cp target/classes com.axisvela.praxo.conformance.ApiSnapshot --check
java -cp target/classes com.axisvela.praxo.conformance.Run
java --add-modules jdk.httpserver -cp target/classes:target/test-classes com.axisvela.praxo.adapters.OpenAICompatibleSelfTest
java -cp target/classes:target/test-classes com.axisvela.praxo.adapters.HarmovelaSinkSelfTest
java -cp target/classes:target/test-classes com.axisvela.praxo.adapters.McpSelfTest
java -cp target/classes:target/test-classes com.axisvela.praxo.agent.AgentConcurrencySelfTest
```

This mirror contains the language source and the shared `spec/` vectors, so the implementation can be built and tested here. See [`language/java/README.md`](language/java/README.md) for the exact commands. The monorepo CI runs conformance, API snapshot, and native tests for this implementation.

## Boundaries

Reference application source is not end-to-end portfolio acceptance; follow each README's scope and evidence.
PRAXO-CORE is not a hosted model, workflow engine, identity provider, or safety controller. Do not infer exactly-once execution, complete sandbox isolation, production security certification, live-provider behavior, or physical safety from this package.

## Community

- X: <https://x.com/axisvela>
- Weibo: <https://weibo.com/u/1936025761>
- LinkedIn: <https://www.linkedin.com/company/axisvela/>
- Facebook: <https://www.facebook.com/profile.php?id=61596905732406>
- YouTube: <https://www.youtube.com/@axisvela>
- Discord: <https://discord.com/channels/1575163993767809064/1575164343148875977>
- GitHub Discussions: <https://github.com/axisvela/praxo-core/discussions>
- GitHub Issues: <https://github.com/axisvela/praxo-core/issues>
- Documentation: <https://axisvela.github.io/praxo-core/>
- Architect: <https://axisvela.architect.pub>

## Repository layout

- `language/java/` — implementation source, tests, API snapshot, and examples
- `spec/` — shared contract, vectors, and parity inventories
- `LICENSE` — MIT license

## Canonical source

- Canonical source: https://github.com/axisvela/praxo-core/tree/main/language/java
- Registry introduction: `language/java/REGISTRY.md`
- Machine-readable entry: `language/java/llms.txt` and `language/java/llms.md`
- Mirror repository: https://github.com/axisvela/praxo-core-java
- Release index: https://axisvela.github.io/praxo-core/languages/registry-status/

This repository is a discovery mirror of the canonical Java source. The monorepo remains the source of truth and the release workflow source. The mirror's `main` branch tracks current source, not a release snapshot. Source tags refer to the canonical monorepo and are not necessarily present in this mirror; syncing the branch does not publish mirror tags or registry packages.


MIT licensed.
