# PRAXO-CORE for Java

Dedicated repository for the Java implementation of PRAXO-CORE: an embeddable,
MIT-licensed agent execution kernel with policy controls, human-in-the-loop
approval, checkpoints, events, and tool calling.

- Package: `com.axisvela:praxo-core:0.4.1` on Maven Central
- Documentation: https://axisvela.github.io/praxo-core/languages/java/
- Consumer starter: https://github.com/axisvela/praxo-core/tree/main/examples/consumer-java
- Canonical source: https://github.com/axisvela/praxo-core/tree/main/language/java
- Release index: https://axisvela.github.io/praxo-core/languages/registry-status/

This repository is a discovery mirror of the canonical Java source. The monorepo
remains the source of truth and the release workflow source. Shared conformance
vectors are included under `spec/`.

## Install

```xml
<dependency>
  <groupId>com.axisvela</groupId>
  <artifactId>praxo-core</artifactId>
  <version>0.4.1</version>
</dependency>
```

## Verify

From `language/java`:

```sh
mvn test
mvn -q -DskipTests package
java -cp target/classes com.axisvela.praxo.conformance.Run
```

PRAXO-CORE is not a hosted model, workflow engine, identity provider, or safety
controller. Do not infer exactly-once execution, complete sandbox isolation,
production security certification, live-provider behavior, or physical safety
from this package.

MIT licensed.
