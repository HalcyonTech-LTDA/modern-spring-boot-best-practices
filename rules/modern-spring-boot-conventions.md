---
description: Automatically enforces modern Spring Boot 3.x+ microservice conventions: strict constructor injection, record-based ConfigurationProperties, strict placeholder discipline without default fallback values (.env.example discipline), RFC 7807 ProblemDetail, RestClient, JdbcClient, and Testcontainers @ServiceConnection.
trigger: model_decision
---

# Modern Spring Boot Guardrails & Skill Router

When modifying, generating, refactoring, or testing Spring Boot 3.x+ applications, strictly adhere to Modern Spring Boot Standards and the corresponding specialized skill:

| When working on... | Consult & Activate Skill | Key Focus Areas |
| :--- | :--- | :--- |
| **Spring Boot Conventions & Patterns** | `modern-spring-boot-conventions` | Constructor injection, record-based `@ConfigurationProperties`, strict placeholder discipline, RFC 7807 `ProblemDetail`, `RestClient`, `JdbcClient`, Virtual Threads, and `@ServiceConnection`. |

---

## Non-Negotiable Guardrails (Absolute Invariants)

1. **Strict Constructor Injection**: Mandate constructor injection for all Spring managed components. Prohibit field-level injection (`@Autowired` on fields).
2. **Type-Safe Configuration & Strict Placeholder Discipline**: Bind configuration properties exclusively using immutable Java `record`s annotated with `@ConfigurationProperties` (prohibit `@Value`). Placeholders in code and configuration files must never define inline default fallback values; all defaults must reside in `.env.example`.
3. **Modern Clients over Deprecated Templates**: Mandate fluent `RestClient` and `JdbcClient` over legacy `RestTemplate` and raw `JdbcTemplate`.
4. **Standardized Web & Error Contracts**: Use specific HTTP mapping annotations (`@GetMapping`, `@PostMapping`). Handle exceptions centrally via `@RestControllerAdvice` emitting RFC 7807 `ProblemDetail` responses.
5. **Deterministic Testing & Connection Slices**: Use slice testing (`@WebMvcTest`, `@DataJpaTest`) and `@ServiceConnection` for Testcontainers. Prefer in-memory fakes or `@MockitoBean` over deprecated `@MockBean`.
6. **Virtual Threads Compatibility**: Write application code ensuring non-blocking execution and full compatibility with enabled Virtual Threads (`spring.threads.virtual.enabled=true`).

Consult the `modern-spring-boot-conventions` skill for complete design patterns, recipes, and detailed guides.
