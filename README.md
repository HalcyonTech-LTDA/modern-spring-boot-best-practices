# Modern Spring Boot Best Practices Plugin

An Antigravity plugin providing automated engineering guardrails, architectural patterns, and specialized skills for modern Spring Boot 3.x+ microservices: strict constructor injection, immutable record-based configuration properties, strict placeholder discipline without default fallback values, RFC 7807 Problem Details, fluent `RestClient` and `JdbcClient` APIs, Java 21 Virtual Threads, and Testcontainers `@ServiceConnection`.

---

## Installation

Install directly in Antigravity via the CLI:

```bash
agy plugin install https://github.com/HalcyonTech-LTDA/modern-spring-boot-best-practices
```

Verify that the plugin is installed and active:

```bash
agy plugin list
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

## What's Included

### 1. Automatic Guardrails (`rules/AGENTS.md`)
Automatically enforced across Spring Boot projects:
- **Constructor Injection Exclusively**: Implicit constructor injection on immutable components; `@Autowired` on fields is strictly prohibited.
- **Zero Framework Leakage in Business Domain**: Core domain models and use case interactors remain 100% pure Java without Spring annotations.
- **Strict Placeholder & Environment Discipline**:
  - In Java classes, placeholders must reference Spring property keys without default fallbacks (`${app.bar.foo}`, never `${APP_BAR_FOO}` or `${app.bar.foo:1s}`).
  - In `application.yaml`, properties point to environment variables without default fallbacks (`app.bar.foo: ${APP_BAR_FOO}`, never `${APP_BAR_FOO:1s}`).
  - All environment variables and sample defaults must be documented in `.env.example` at the repository root.
- **Record-Based Configuration**: External configurations are mapped to immutable Java `record`s with `@ConfigurationProperties` discovered via `@ConfigurationPropertiesScan`.
- **RFC 7807 Problem Details**: Standardized REST error responses using `ProblemDetail` via `@RestControllerAdvice`.
- **Modern Fluent Clients**: Fluent `RestClient` for HTTP and `JdbcClient` for direct SQL queries.
- **Virtual Threads Policy**: Ensuring non-blocking virtual thread execution without carrier thread pinning.
- **Deterministic Testing**: Slices over monolithic `@SpringBootTest`, Testcontainers `@ServiceConnection`, and `@MockitoBean` over deprecated `@MockBean`.

### 2. Specialized Skills (`skills/`)

#### 🍃 `modern-spring-boot-conventions`
Guides authoring, refactoring, and reviewing Spring Boot 3.x+ applications:
- Clean dependency injection and separation of concerns.
- Type-safe, validated configuration records.
- Modern HTTP communication with declarative and fluent `RestClient`.
- High-performance data access with `JdbcClient` and `ListCrudRepository`.
- Virtual thread configuration and carrier-pinning diagnostics.
- Sliced testing architectures and Testcontainers choreography.

---

## Directory Layout

```text
modern-spring-boot-best-practices/
├── plugin.json
├── README.md
├── LICENSE
├── .gitignore
├── .gitattributes
├── rules/
│   └── AGENTS.md
└── skills/
    └── modern-spring-boot-conventions/
        └── SKILL.md
```

---

## License

This project is licensed under the [MIT License](LICENSE) - see the LICENSE file for details.
Copyright (c) 2026 Halcyon Tech.
