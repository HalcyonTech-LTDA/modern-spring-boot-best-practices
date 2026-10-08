---
description: Automatically enforces modern Spring Boot 3.x+ microservice conventions: strict constructor injection, record-based ConfigurationProperties, strict placeholder discipline without default fallback values (.env.example discipline), RFC 7807 ProblemDetail, RestClient, JdbcClient, and Testcontainers @ServiceConnection.
trigger: model_decision
---

# Spring Boot Conventions Rule

When modifying or creating Spring Boot components, strictly adhere to the `modern-spring-boot-conventions` skill. 

Key automatic enforcement points:
- **Injection**: Always use constructor injection. Never use `@Autowired` on fields.
- **Properties & Placeholders**: Always use Records with `@ConfigurationProperties` (never `@Value`). Placeholders in Java classes must reference property keys without default values (e.g. `${app.bar.foo}`, never `${APP_BAR_FOO}` or `${app.bar.foo:1s}`). In `application.yaml`, properties point to environment variables without default values (e.g. `app.bar.foo: ${APP_BAR_FOO}`, never `${APP_BAR_FOO:1s}`). All environment variables and their default/sample values must be defined in `.env.example` at the project root.
- **Controllers**: Always use specific mapping annotations (`@GetMapping`, etc.) and handle errors via `@RestControllerAdvice` emitting RFC 7807 `ProblemDetail`.
- **Clients**: Use `RestClient` and `JdbcClient` over their legacy `Template` counterparts.
- **Tests**: Use slice testing (`@WebMvcTest`, etc.) and `@ServiceConnection` for Testcontainers. Prefer `@MockitoBean` over the deprecated `@MockBean` (if mocking is absolutely necessary instead of faking).
- **Concurrency**: Write code keeping in mind that Virtual Threads are enabled (`spring.threads.virtual.enabled=true`).

Consult the `modern-spring-boot-conventions` skill for complete details if unsure.
