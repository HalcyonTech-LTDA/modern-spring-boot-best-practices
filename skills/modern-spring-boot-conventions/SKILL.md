---
name: modern-spring-boot-conventions
description: Use this skill when developing, refactoring, or reviewing Spring Boot 3.x+ applications. Covers Spring-specific best practices, including configuration, DI, REST controllers, data access, Observability, and modern APIs (RestClient, JdbcClient).
---

# Modern Spring Boot Conventions & Best Practices

This skill outlines the standard baseline for modern Spring Boot 3.x+ applications. It focuses exclusively on the Spring ecosystem, complementing general modern Java, OOP, and Clean Architecture practices.

## 1. Dependency Injection
*   **Constructor Injection Exclusively:** Never use `@Autowired` on fields. Rely on implicit constructor injection (or standard Java constructors/records) to make dependencies explicit, immutable, and easy to inject during unit testing without reflection.
*   **Avoid Framework Coupling in Core Domain:** Keep Spring annotations completely out of the core domain logic (Entities, Use Cases/Interactors). Use them only in Framework adapters and Configuration classes.

## 2. Configuration & Properties
*   **Strict Placeholder & Environment Discipline**:
    *   **Inside Java Classes**: Any placeholder used in annotations (e.g. `@Scheduled`, `@KafkaListener`, `@ConditionalOnProperty`) must reference a **Spring property key**, NEVER an environment variable directly. Example: `${app.bar.foo}` ✅ (NEVER `${APP_BAR_FOO}` ❌).
    *   **Inside `application.yaml` (or `.properties`)**: Properties that depend on external environment variables must map directly to the environment variable via placeholder: `app.bar.foo: ${APP_BAR_FOO}` ✅.
    *   **Prohibition of Default Fallback Values in Placeholders**: Placeholders must NEVER contain default fallback values (e.g., `${app.bar.foo:1s}` ❌ or `app.bar.foo: ${APP_BAR_FOO:1s}` ❌ are strictly forbidden). They must always be declared strictly as `${app.bar.foo}` in Java and `app.bar.foo: ${APP_BAR_FOO}` in YAML.
    *   **Values Declared in `.env.example`**: The actual value, default, or example for the environment variable must be documented and defined in the `.env.example` file located at the project root (e.g., `APP_BAR_FOO=1s`).
*   **Record-Based `@ConfigurationProperties`:** Bind external configuration properties to immutable Java Records using `@ConfigurationProperties`. 
*   **Enable via Scan:** Use `@ConfigurationPropertiesScan` at the application level instead of explicitly defining `@EnableConfigurationProperties` for each property class.
*   **Avoid `@Value`:** Do not use `@Value` for property injection, as it scatters configuration across the codebase and lacks strong typing and validation compared to dedicated property records.

## 3. Web & REST APIs
*   **Modern Web Clients:** Use the fluent `RestClient` (introduced in Spring Boot 3.2) instead of the legacy `RestTemplate` for synchronous HTTP calls.
*   **Standardized Error Handling:** Enable RFC 7807 Problem Details (`spring.mvc.problemdetails.enabled=true`). Use `@RestControllerAdvice` to map domain exceptions to `ProblemDetail` or `ErrorResponse` objects. Avoid inventing custom error response envelopes.
*   **Explicit Mapping:** Prefer specific annotations like `@GetMapping`, `@PostMapping`, etc., over the generic `@RequestMapping`.

## 4. Data Access
*   **Modern JDBC Client:** When interacting with SQL directly without an ORM, prefer the fluent `JdbcClient` over `JdbcTemplate` for a safer and more readable API.
*   **Transaction Boundaries:** Apply `@Transactional` strictly at the service or use-case boundary. Use `@Transactional(readOnly = true)` for query-only operations to enable database driver optimizations.
*   **Spring Data Collections:** When using Spring Data, prefer specific repository interfaces like `ListCrudRepository` or `ListPagingAndSortingRepository` instead of the legacy `CrudRepository` so you can work with `List` rather than `Iterable`.

## 5. Concurrency & Performance
*   **Virtual Threads:** Enable Java 21 Virtual Threads globally using `spring.threads.virtual.enabled=true`. Ensure I/O blocking operations are virtual-thread friendly and avoid pinning carrier threads (e.g., synchronized blocks wrapping I/O).
*   **AOT & Native Readiness:** Write code that is friendly to GraalVM Native Image. Minimize reflection, dynamic proxies, and complex SpEL expressions where simpler programmatic alternatives exist.

## 6. Testing (Spring Slices & Testcontainers)
*   **Test Slices:** Prefer focused slice tests (`@WebMvcTest`, `@DataJpaTest`, `@DataJdbcTest`) over loading the full context with `@SpringBootTest` to keep the test suite fast.
*   **Testcontainers with `@ServiceConnection`:** Use Spring Boot 3.1+ `@ServiceConnection` for seamless Testcontainers integration. Avoid manually managing container properties.
*   **Mocking:** Use `@MockitoBean` and `@MockitoSpyBean` (Spring Boot 3.4+) instead of the deprecated `@MockBean` / `@SpyBean`. Note: Prefer using in-memory fakes over mocks as defined in general testing guidelines, using these annotations only when fakes are not practical.

## 7. Observability & Actuator
*   **Micrometer Observations:** Use Micrometer's `@Observed` annotation and the `ObservationRegistry` for tracking service-level metrics and distributed tracing.
*   **Actuator Endpoints:** Expose standard actuator endpoints (`health`, `info`, `prometheus`) to integrate seamlessly with cloud-native monitoring stacks.
