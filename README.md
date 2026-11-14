# PRAXO-CORE for Java

Java implementation of the PRAXO-CORE contract. The normative contract is [`spec/`](spec/README.md); Go remains the reference implementation.

## At a glance

| Field | Value |
| --- | --- |
| Package | `com.axisvela:praxo-core` |
| Registry | [Maven Central](https://repo1.maven.org/maven2/com/axisvela/praxo-core/0.9.0/) |
| Install | `Maven: com.axisvela:praxo-core:0.9.0` |
| Source version | `0.10.0` |
| Published version | `0.9.0` |
| Source tag | `java/v0.10.0` |
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
Maven: com.axisvela:praxo-core:0.9.0
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
| Anthropic model | native | `adapters.AnthropicModel` |
| Gemini model | native | `adapters.GeminiModel` |
| MCP client | native | `adapters.McpClient`; stdio, plus `McpStreamableHttpTransport` for Streamable HTTP 2025-03-26 (local runtime verification pending) |
| Harmovela sink | native | `adapters.HarmovelaSink` |
| OpenTelemetry sink | native (transport seam) | `adapters.OtelSink`; caller supplies OTLP/HTTP transport |
| Subagent delegation | native | `agent.delegation.SubagentManager` |
| Retriever | native | `retriever.Document` and `Retriever` |

## Examples

Runnable examples live under [`language/java/examples`](language/java/examples).

| Example | What it shows |
| --- | --- |
| [checkpoint](language/java/examples/checkpoint) | This example uses published Maven `com.axisvela:praxo-core:0.7.0` to keep checkpoint storage application-owned while using the SDK allowlist for payload encoding. |
| [consumer](language/java/examples/consumer) | This starter installs the published `com.axisvela:praxo-core:0.9.0` artifact from Maven Central in a separate application. It does not compile or import the repository's Java so... |
| [event-sink](language/java/examples/event-sink) | This example uses published Maven `com.axisvela:praxo-core:0.7.0` to observe agent lifecycle and tool events without coupling the agent to a logging or telemetry backend. |
| [identity-policy](language/java/examples/identity-policy) | This example uses published Maven `com.axisvela:praxo-core:0.7.0` to bind a trusted principal to Core policy authorization. The application owns authentication and principal sto... |
| [live-model](language/java/examples/live-model) | This example uses published Maven Central `com.axisvela:praxo-core:0.9.0` to connect the Java Core to an OpenAI-compatible endpoint and registers one low-risk `get_time` tool. |
| [mcp](language/java/examples/mcp) | This example uses published Maven `com.axisvela:praxo-core:0.7.0` with an in-process `McpTransport`. It needs no server process and no network endpoint. |
| [provider-fallback](language/java/examples/provider-fallback) | This example uses published Maven `com.axisvela:praxo-core:0.7.0` to fall back to a second model when the primary model call fails. |
| [retry](language/java/examples/retry) | This example uses published Maven `com.axisvela:praxo-core:0.7.0` to retry transient model failures without changing the agent loop. |
| [service](language/java/examples/service) | This example embeds published Maven `com.axisvela:praxo-core:0.7.0` in a standard-library JDK HTTP service. The application supplies a principal and tenant, restricts tools, and... |
| [streaming](language/java/examples/streaming) | This example uses published Maven `com.axisvela:praxo-core:0.7.0` to consume deltas while the agent loop keeps running normally. |
| [structured-output](language/java/examples/structured-output) | This example uses published Maven Central `com.axisvela:praxo-core:0.7.0` to turn free text into validated JSON with `StructuredOutput`. |

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

## Community

- X: <https://x.com/axisvela>
- Weibo: <https://weibo.com/u/1936025761>

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

This repository is a discovery mirror of the canonical Java source. The monorepo remains the source of truth and the release workflow source.

PRAXO-CORE is not a hosted model, workflow engine, identity provider, or safety controller. Do not infer exactly-once execution, complete sandbox isolation, production security certification, live-provider behavior, or physical safety from this package.

MIT licensed.
