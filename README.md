<div align="center">

# Modern Spring Boot Best Practices Plugin
### Spring Boot 3.x+ Microservice Architecture, RestClient & ProblemDetail

[![Antigravity Plugin](https://img.shields.io/badge/Antigravity-Plugin%20v1.0.0-4F46E5.svg)](https://antigravity.google)
[![License: MIT](https://img.shields.io/badge/License-MIT-10B981.svg)](./LICENSE)
[![Organization](https://img.shields.io/badge/Organization-HalcyonTech--LTDA-black.svg)](https://github.com/HalcyonTech-LTDA)

<p align="center">
  <b>Modern Spring Boot 3.x+ microservice conventions and best practices: strict constructor injection, immutable configuration records, placeholder discipline without default fallback values (.env.example discipline), RFC 7807 ProblemDetail error handling, fluent RestClient & JdbcClient APIs, Testcontainers @ServiceConnection, and cloud-native Micrometer observability.</b>
</p>

</div>

---

## Installation & Verification

### Antigravity CLI (`agy`)

Install directly into your Antigravity environment via the CLI:

```bash
agy plugin install https://github.com/HalcyonTech-LTDA/modern-spring-boot-best-practices
```

Verify that the plugin is active and adheres to the strict official schema:

```bash
agy plugin list
agy plugin validate --strict ./modern-spring-boot-best-practices
```

---

## Overview

Modern Spring Boot 3.x+ application development demands lean framework coupling, strong immutability, deterministic configuration management, and native-first Java 21 integration. This plugin enforces production-grade conventions across seven fundamental pillars:

1. **Dependency Injection**: Constructor injection exclusively; absolute ban on field injection (`@Autowired`).
2. **Configuration & Placeholders**: Record-based `@ConfigurationProperties`, ban on `@Value`, and strict placeholder discipline without default fallback values (driven by `.env.example`).
3. **Web & REST APIs**: Fluent `RestClient` over legacy `RestTemplate`, and RFC 7807 `ProblemDetail` error handling with `@RestControllerAdvice`.
4. **Data Access**: Fluent `JdbcClient` over legacy `JdbcTemplate`, transaction boundary discipline, and `ListCrudRepository`.
5. **Concurrency & Performance**: Native Java 21 Virtual Threads (`spring.threads.virtual.enabled=true`) and GraalVM AOT readiness.
6. **Testing**: Fast slice testing (`@WebMvcTest`, `@DataJpaTest`), Testcontainers with `@ServiceConnection`, and `@MockitoBean`.
7. **Observability**: Micrometer Observation registry, structured distributed tracing, and Actuator endpoints.

---

---

## What's Included (Component Catalog)

### Contextual Rules (`rules/`)
Automatically loaded to govern and protect project contexts:
- **[`modern-spring-boot-conventions.md`](rules/modern-spring-boot-conventions.md)**: Automatically enforces modern Spring Boot 3.x+ microservice conventions: strict constructor injection, record-based ConfigurationProperties, strict placeholder discipline without default fallback values (.env.example discipline), RFC 7807 ProblemDetail, RestClient, JdbcClient, and Testcontainers @ServiceConnection.

### Procedural Skills (`skills/`)
On-demand actionable workflows and runbooks:
- **[`/modern-spring-boot-conventions`](skills/modern-spring-boot-conventions/SKILL.md)**: Use this skill when developing, refactoring, or reviewing Spring Boot 3.x+ applications. Covers Spring-specific best practices, including configuration, DI, REST controllers, data access, Observability, and modern APIs (RestClient, JdbcClient).

---

## Directory Hierarchy

```text
modern-spring-boot-best-practices/
├── plugin.json              # Official Antigravity manifest (schema v1)
├── LICENSE                  # MIT License (Copyright 2026 HalcyonTech LTDA)
├── .gitignore               # System ignores & installed_version.json exclusions
├── .gitattributes           # Deterministic line endings (* text=auto eol=lf)
├── README.md                # Golden Standard documentation & runbook
├── assets/
│   └── logo.svg             # Official Halcyon Tech corporate vector symbol
├── rules/                   # Contextual rules discovered automatically
│   └── modern-spring-boot-conventions.md
├── skills/                  # Actionable procedural skills (Progressive Disclosure)
│   └── modern-spring-boot-conventions/
│       └── SKILL.md
```

---

## 💡 Prompt Recipes & Use Cases

```markdown
- "Refactor Spring Boot service to strict constructor injection and RestClient"
- "Implement RFC 7807 ProblemDetail error handling and record ConfigurationProperties"
- "Set up integration testing with Testcontainers and @ServiceConnection"
```

---

## 📄 License & Corporate Governance

Distributed under the **MIT License**. Copyright (c) 2026 **HalcyonTech LTDA**.  
Engineered with precision and excellence by [Halcyon Tech](https://github.com/HalcyonTech-LTDA).
